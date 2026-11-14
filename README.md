# `@openOODA/catalog`

Signed package registry and layer manifest index (`L0`–`L7`) queried by [`oopm`](https://github.com/openOODA-core/oopm) for [openOODA](https://openOODA.org).

[![OODAC on StartupScores](https://startupscores.com/badge/oodac.svg?style=shield&v=combo&theme=dark)](https://startupscores.com/open-source/oodac)

## Structure

```text
catalog/
├── AGENTS.md
├── README.md
├── Makefile        # build / verify / test / sync / sums gates
├── ooda.pkg        # catalog package manifest (name=catalog, entry=cli/main.oo)
├── anchor.oo       # root anchor re-exporting core/ conformance pages
├── cli/
│   └── main.oo     # catalog binary: verify, sync, theme, about
├── core/
│   ├── cat_manifest.oo  # manifest field + payload-digest conformance
│   └── cat_index.oo     # descriptor emitter + index/groups/sums/sig gates
├── tests/
│   ├── test_functional.oo  # 12 positive assertions over the signed tree
│   └── test_refusal.oo     # 11 forged/missing/tamper refusal probes
├── groups.oot      # Fedora-style @group profiles (@core..@agents, @workstation, @all)
├── index           # Package index rows (name|version|caps|deps|sha256)
├── index.sig       # HMAC-SHA256 signature over index
├── registry.pub    # Registry verification public key
├── SHA256SUMS      # Master checksums mirrored from the install@hub release
└── layers/
    ├── L0-core/    # 8 core toolchain packages (ooda, oodac, oodar, oostd, oopm, oolsp, oomcp, oohat)
    ├── L1-kernel/  # 8 microkernel, bootloader, HAL & Ring-3 driver packages
    ├── L2-OS/      # 9 zero-root system daemon packages
    ├── L3-tools/   # 39 capability-sandboxed Unix, security & UI utilities (incl. ootheme)
    ├── L4-DE/      # 8 Wayland desktop environment packages
    ├── L5-apps/    # 16 native desktop, creative & gaming applications
    ├── L6-cloud/   # 8 mesh, storage, deploy, DB & gateway services
    └── L7-agents/  # 9 autonomous OODA loop, dream & verification packages
```

Each `layers/<layer>/<pkg>/` directory holds a `manifest` (name, version,
caps, deps, payload, sha256) and a `<pkg>.oo` **signed descriptor** — a
canonical constant-surface page emitted byte-for-byte by
`core/cat_index.oo`'s `cat_descriptor`. The `index` row's `sha256` binds the
manifest, the descriptor bytes, and the signed entry together; nothing in the
tree is trusted without recomputation (`./bin/catalog verify .`).

`oostd` (L0) ships the expanded scientific & mathematical discovery library:
`oostd/core/math/{exact,geometry,blas,fft,algebra,graph_topology}/...`,
`oostd/core/proofs/...`, `oostd/core/science/{phys,chem,bio,comm,econ}/...`,
frontier AI-for-science `oostd/core/app/ai/...`, 2D/3D engine physics
`oostd/core/app/ui/game_engine/...` (`collision_{aabb,circle,gjk,sat}` + `ecs_*`),
`oostd/core/collection/...`, and `oostd/sec/{hash,capability,pqc,symmetric}/...`.

## Building & Verifying

```sh
make build        # compile cli/main.oo -> bin/catalog (oodac)
make test         # functional + refusal suites + catalog verify under PATH=/nonexistent
make verify       # page/file/academy/density/vocab/shape/link/oodac gates + catalog verify
./bin/catalog verify .   # index<->dirs->manifest->descriptor->digest + groups + sums + sig
./bin/catalog sync .     # re-derive descriptors, manifests, index + index.sig deterministically
```

## Installing Packages & Groups with `oopm`

```sh
oopm search <query>
oopm install <package>
oopm group list
oopm install @core
oopm install @tools
oopm install @workstation
oopm install @all
```
