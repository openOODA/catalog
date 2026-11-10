# catalog (openOODA) — Signed Package Index & Group Profiles

Canonical signed registry of the openOODA `L0`–`L7` package set, consumed by
[`oopm`](https://github.com/openOODA-core/oopm) resolve/install and mirrored
onto the `openOODA/install@hub` release. `catalog` is an index/profile/manifest
repository — it signs *package descriptors*, never package implementations.
Real package source lives in the per-org sibling repos
(`/Projects/openOODA-*/<pkg>`); this tree holds only the registry surface that
binds them.

## Exact Boundary

`catalog` owns exactly these 14 root entries, and nothing else:

- `index` — one `name|version|caps|deps|sha256` row per active package.
- `index.sig` — HMAC-SHA256 (`ooda-local-pm`) over the `index` body bytes.
- `registry.pub` — registry verification public key (minisign).
- `groups.oot` — `@group` selection profiles (`@core @kernel @os @tools @de @apps @cloud @agents @workstation @all`).
- `SHA256SUMS` — master checksums mirrored from the published `install@hub` release assets.
- `layers/` — exactly 8 layer dirs, `layers/L<x>/<pkg>/{manifest,<pkg>.oo}` per package.
- `cli/main.oo` — the `catalog` binary (`verify`, `sync`, `theme`, `about`).
- `core/cat_manifest.oo`, `core/cat_index.oo` — manifest + index conformance checkers.
- `tests/` — the lean 2-file suite (`test_functional.oo`, `test_refusal.oo`).
- `anchor.oo`, `AGENTS.md`, `README.md`, `Makefile`, `ooda.pkg` — repo surface.

Out of scope: package implementations, upstream `dist/` binaries, release
staging (`/Projects/openOODA/install/publish-hub.sh` owns that), telemetry,
secrets, and any network/process authority.

## Invariants (Zero Trust — fail closed, byte-exact)

1. **Index <-> dirs bijection**: every `index` row resolves to exactly one
   `layers/<layer>/<name>` dir, and every package dir appears in exactly one
   row. `cat_index_scan` + `cat_dirs_indexed` prove both directions.
2. **Manifest conformance**: `manifest` `name=` equals its directory basename;
   `payload=` is an in-package path (any `..` refused); `sha256=` is 64-hex and
   equals `sha256_hex` of the payload bytes (`cat_manifest_ok`).
3. **Canonical descriptors**: each `<pkg>.oo` payload is the *signed
   descriptor* — the byte-for-byte output of `cat_descriptor(name, layer,
   version, caps, deps)` in `core/cat_index.oo`. A payload that is not the
   canonical emission fails `cat_index_ok` even if its digest matches.
4. **Row<->manifest agreement**: index `version|caps|deps|sha256` equal the
   manifest fields exactly; the index `sha256` additionally equals the payload
   digest. `index.sig` must re-derive over the current index body.
5. **Group coverage**: every package appears exactly once in its layer's
   `@group` line (`@tools` <-> `L3-tools`, ...); `@games` is a subset of
   `@apps`; `@workstation = @core @tools @de @apps`; `@all` expands all 8
   layer groups.
6. **Sums parity**: every `SHA256SUMS` line is `<64-hex>  <asset>` where the
   asset stem (`<pkg>-linux-x86_64`, `liboodar.a` -> `oodar`,
   `oostd-linux-x86_64.tar.gz` -> `oostd`, or the two aux images
   `ooda-os-x86_64.iso` / `ooda-buildbox-x86_64.tar.gz`) maps to a real index
   package; no stale, foreign, malformed, or duplicate lines.
7. **Retired packages never appear**: `ooagent-hud` (folded into `oopanel`),
   `ooquota` (folded into `oogovern`), `oofetch`, `ootop` and similar retired
   names must not exist in `index`, `groups.oot`, `layers/`, or `SHA256SUMS`.
8. **Generation, not trust**: `catalog sync .` re-derives every descriptor,
   manifest, `index`, and `index.sig` deterministically from the current rows;
   `catalog verify .` recomputes all of it read-only and exits 1 on any gap.

## Power-of-2 Shape Ladder

`1` link count / stmt-per-line, `2` lean tests, `4` nesting depth, `8`
files/dir + fns/file + params/fn, `16` min lines/file (import shims exempt),
`32` char names, `64` code lines/fn, `128` chars/line, `256` lines/file.

## Build & Verify

```sh
make build && make test            # bin/catalog + functional/refusal suites + verify
make verify                        # full page/file/academy/shape/link/oodac + catalog gates
make sync                          # regenerate descriptors/manifests/index/index.sig
./bin/catalog verify .             # PASS: catalog verify (105 packages)
/Projects/openOODA-core/oohat/bin/oohat cycle /Projects/openOODA/catalog   # quorum_mask=255 required
```
