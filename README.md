# `@openOODA/catalog`

Signed package registry and layer manifest index (`L0`–`L7`) queried by [`oopm`](https://github.com/openOODA-core/oopm) for [openOODA](https://openOODA.org).

## Structure

```text
catalog/
├── AGENTS.md
├── README.md
├── groups.oot      # Fedora-style @group profiles (@core..@agents, @workstation, @all)
├── index           # Package index rows (name|version|caps|deps|sha256)
├── index.sig       # HMAC-SHA256 signature over index
├── registry.pub    # Registry verification public key
├── SHA256SUMS      # Master checksums mirrored from the install@hub release
└── layers/
    ├── L0-core/    # 8 core toolchain packages (ooda, oodac, oodar, oostd, oopm, oolsp, oomcp, oohat)
    ├── L1-kernel/  # 8 microkernel, bootloader, HAL & Ring-3 driver packages
    ├── L2-OS/      # 9 zero-root system daemon packages
    ├── L3-tools/   # 39 capability-sandboxed Unix, security & UI utilities
    ├── L4-DE/      # 8 Wayland desktop environment packages
    ├── L5-apps/    # 16 native desktop, creative & gaming applications
    ├── L6-cloud/   # 8 mesh, storage, deploy, DB & gateway services
    └── L7-agents/  # 9 autonomous OODA loop & verification packages
```

`oostd` (L0) ships the expanded scientific & mathematical discovery library:
`oostd/core/math/{exact,geometry,blas,fft,algebra,graph_topology}/...`,
`oostd/core/proofs/...`, `oostd/core/science/{phys,chem,bio,comm,econ}/...`,
frontier AI-for-science `oostd/core/app/ai/...`, 2D/3D engine physics
`oostd/core/app/ui/game_engine/...` (`collision_{aabb,circle,gjk,sat}` + `ecs_*`),
`oostd/core/collection/...`, and `oostd/sec/{hash,capability,pqc,symmetric}/...`.

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
