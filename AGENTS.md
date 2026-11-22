# catalog (openOODA) — Signed Package Index & Group Profiles

Canonical signed registry of the openOODA 4-organization, 72-package set
(`openOODA-core` 15, `openOODA-system` 37, `openOODA-apps` 20), queried by
[`ooda-package`](https://github.com/openOODA-core/ooda-package) resolve/install
and mirrored onto the `openOODA/install@hub` release. `catalog` is an
index/profile/manifest repository — it signs *package descriptors*, never
package implementations. Real package source lives in the per-org sibling
repos (`$OODA_POLYROOT/openOODA-*/<pkg>`); this tree holds only the registry
surface that binds them.

## Exact Boundary

`catalog` owns exactly these 15 root entries, and nothing else:

- `AGENTS.md`, `README.md`, `Makefile`, `ooda.pkg`, `anchor.oo` — repo surface.
- `COMMIT_LEDGER` — canonical commit SHA map across all 72 product repos.
- `index` — one `name|version|caps|deps|sha256` row per active package (72 rows).
- `index.sig` — HMAC-SHA256 (`ooda-local-pm`) over the `index` body bytes.
- `registry.pub` — registry verification public key (minisign).
- `groups.oot` — `@group` selection profiles (`@core @system @apps @games @desktop @workstation @all`).
- `SHA256SUMS` — master checksums mirrored from the published `install@hub` release assets.
- `layers/` — exactly 3 layer dirs (`core/`, `system/`, `apps/`), `<pkg>/{manifest,<pkg>.oo}` per package.
- `cli/main.oo` — the `catalog` binary (`verify`, `sync`, `theme`, `about`).
- `core/cat_manifest.oo`, `core/cat_index.oo`, `core/sums_sib.oo` — manifest + index conformance checkers.
- `tests/` — the lean 2-file suite (`test_functional.oo`, `test_refusal.oo`).

Out of scope: package implementations, upstream `dist/` binaries, release
staging (`$OODA_POLYROOT/openOODA/install/publish-hub.sh` owns that), telemetry,
secrets, and any network/process authority.

## Invariants (Zero Trust — fail closed, byte-exact)

1. **Index <-> dirs bijection**: every `index` row resolves to one
   `layers/{core,system,apps}/<name>` dir, and every package dir appears in
   one row. `cat_index_scan` + `cat_dirs_indexed` prove both directions.
2. **Manifest conformance**: `manifest` `name=` equals its directory basename;
   `payload=` is an in-package path (`..` refused); `sha256=` is 64-hex and
   equals `sha256_hex` of the payload bytes (`cat_manifest_ok`).
3. **Canonical descriptors**: each `<pkg>.oo` payload is the *signed
   descriptor* — the byte-for-byte output of `cat_descriptor(name, layer,
   version, caps, deps)` in `core/cat_index.oo`. A payload that is not the
   canonical emission fails `cat_index_ok` even if its digest matches.
4. **Row <-> manifest agreement**: index `version|caps|deps|sha256` equal the
   manifest fields; `index.sig` re-derives over the current `index` body.
5. **Group coverage**: every package appears in its org group (`@core` <->
   `core/`, `@system` <-> `system/`, `@apps` <-> `apps/`); `@games` is a
   subset of `@apps`; `@desktop`, `@workstation`, `@all` expand `@core @system @apps`.
6. **Sums parity**: every `SHA256SUMS` line is `<64-hex>  <asset>` where the
   asset stem (`<pkg>-linux-x86_64`, `libooda-runtime*.a` -> `ooda-runtime`,
   `ooda-standard-linux-x86_64.tar.gz` -> `ooda-standard`, or aux assets
   `ooda-os-x86_64.iso`, `ooda-buildbox-x86_64.tar.gz`, `cap_table.oot`) maps
   to a real index package; no stale, foreign, malformed, or duplicate lines.
7. **Retired names never appear**: legacy `L0-core..L7-agents` layers and
   retired `oo*` names (`oostd`, `oodac`, `oodar`, `oopm`, `oolsp`, `oomcp`,
   `oohat`, etc.) must not exist in `index`, `groups.oot`, `layers/`, or `SHA256SUMS`.
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
make verify                        # full page/file/academy/shape/link/ooda-compiler + catalog gates
make sync                          # regenerate descriptors/manifests/index/index.sig
./bin/catalog verify .             # PASS: catalog verify (72 packages)
~/.openooda/bin/ooda-verify cycle . --json   # quorum_mask=255 required
```
