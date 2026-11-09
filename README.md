# `@openOODA/catalog`

Signed package registry and layer manifest index (`L0`–`L7`) queried by [`oopm`](https://github.com/openOODA-core/oopm) for [openOODA](https://openOODA.org).

## Structure

```text
catalog/
├── AGENTS.md
├── README.md
├── VERSION
└── layers/
    ├── L0-core/       # 7 core toolchain packages (ooda, oodac, oodar, oostd, oopm, oolsp, oomcp)
    ├── L1-kernel/     # 6 microkernel, bootloader, HAL & driver packages
    ├── L2-os/         # 9 zero-root system daemon packages
    ├── L3-tools/      # 39 capability-sandboxed Unix, security & UI utilities
    ├── L4-de/         # 8 Wayland desktop environment packages
    ├── L5-apps/       # 16 native desktop, creative & gaming applications
    ├── L6-cloud/      # 8 mesh, storage, deploy, DB & gateway services
    └── L7-agents/     # 10 autonomous OODA loop & verification packages
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
