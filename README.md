# `@openOODA/catalog`

Signed package registry and layer manifest index (`66` packages across `openOODA-core`, `openOODA-system`, `openOODA-apps`, and `openOODA-games`) queried by [`ooda-package`](https://github.com/openOODA-core/ooda-package) for [openOODA](https://openooda.org).

## Structure

```text
catalog/
├── AGENTS.md
├── README.md
├── Makefile        # build / verify / test / sync / sums gates
├── ooda.pkg        # catalog package manifest (name=catalog, version=2.8.0)
├── anchor.oo       # root anchor re-exporting core/ conformance pages
├── COMMIT_LEDGER   # canonical commit SHA ledger across all 66 product repos
├── cli/
│   └── main.oo     # catalog binary: verify, sync, theme, about
├── core/
│   ├── cat_manifest.oo  # manifest field + payload-digest conformance
│   ├── cat_index.oo     # descriptor emitter + index/groups/sums/sig gates
│   └── sums_sib.oo      # sibling persona asset tracer
├── tests/
│   ├── test_functional.oo  # 11 positive assertions over the signed tree
│   └── test_refusal.oo     # 11 forged/missing/tamper refusal probes
├── groups.oot      # @group profiles (@core, @system, @apps, @games, @desktop, @workstation, @all)
├── index           # Package index rows (name|version|caps|deps|sha256)
├── index.sig       # HMAC-SHA256 signature over index
├── registry.pub    # Registry verification public key
├── SHA256SUMS      # Master checksums mirrored from the install@hub release
└── layers/
    ├── core/       # 11 @openOODA-core packages (incl. ooda, ooda-compiler, ooda-runtime, ooda-standard, ooda-package, ooda-language, ooda-bridge, ooda-verify, ooda-version)
    ├── system/     # 27 @openOODA-system OS, kernel, driver, desktop, cloud & AI inference packages
    ├── apps/       # 19 @openOODA-apps native desktop & terminal applications
    └── games/      # 9 @openOODA-games engine & native games titles
```

Each `layers/{core,system,apps,games}/<pkg>/` directory holds a `manifest` and a
`<pkg>.oo` **signed descriptor** — emitted byte-for-byte by `core/cat_index.oo`'s
`cat_descriptor`. The `index` row's `sha256` binds the manifest, descriptor
bytes, and signed entry together; nothing in the tree is trusted without
recomputation (`./bin/catalog verify .`).

`ooda-standard` (`core`) ships the capability-gated standard library (exact math,
geometry, BLAS/FFT, algebra, graph topology, proof helpers, physics/chem/bio, AI
primers, 2D/3D engine physics, collections, PQC/AEAD crypto, and `ootheme`).

## Building & Verifying

```sh
make build        # compile cli/main.oo -> bin/catalog (ooda-compiler)
make test         # functional + refusal suites + catalog verify under PATH=/nonexistent
make verify       # page/file/academy/density/vocab/shape/link/compiler gates + catalog verify
./bin/catalog verify .   # index<->dirs->manifest->descriptor->digest + groups + sums + sig
./bin/catalog sync .     # re-derive descriptors, manifests, index + index.sig deterministically
```

## Installing Packages & Groups with `ooda-package`

```sh
ooda-package search <query>
ooda-package install <package>
ooda-package group list
ooda-package install @core
ooda-package install @system
ooda-package install @apps
ooda-package install @games
ooda-package install @workstation
ooda-package install @all
```
