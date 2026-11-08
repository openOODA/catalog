<div align="center">

<pre>
   ____  ____  ___  ____    ___   ___  ____    _
  / __ \/ __ \/ _ \/ __ \  / _ \ / _ \|  _ \  / \
 / /_/ / /_/ /  __/ / / / | | | | | | | | | |/ _ \
/_____/ .___/\___/_/ /_/  | |_| | |_| | |_| / ___ \
      /_/                   \___/ \___/|____/_/   \_\
</pre>

### `catalog` — Cryptographically signed public package catalog and Fedora-style @group index for the 93 openOODA packages.

[openooda.org](https://openooda.org) • [`openOODA/catalog`](https://github.com/openOODA/catalog) • [Public Binary Hub (`install@hub`)](https://github.com/openOODA/install/releases/tag/hub) • [Governance & Quick Cards (`openOODA/openOODA`)](https://github.com/openOODA/openOODA)

</div>

---

## Overview

**`catalog`** (`v0.2.6`) is a canonical repository in **Root (`@openOODA`)** of the [openOODA](https://github.com/openOODA) capability-secured computing stack (`L0`–`L7`).

- **Description**: Cryptographically signed public package catalog and Fedora-style @group index for the 93 openOODA packages.
- **Layer & Bundle**: Root (`@openOODA`) • Fedora-style bundle `@core` (`oopm install @core` or `oopm install catalog`)
- **Explicit Capabilities (`CapReg64`)**: `FsReadCap`, `FsWriteCap`, `EnvCap`, `ProcessCap`, `TcpCap`, `FfiCap`, `BindCap`, `TimeCap`
- **Security & CISA KEV Posture**: Hardened against `CWE-22` (path traversal admission), `CWE-78` (shell-free argv execution), `CWE-190`/`CWE-787` (checked bounds arithmetic), and `CWE-502` (depth-bounded `.oot` deserialization); verified under the 8-Hat adversarial consensus engine (`oohat cycle` `quorum_mask=255`) and deterministic double-compilation (`make det`).
- **Theme & Surface Integration**: Wired to [`ootheme`](https://github.com/openOODA-tools/ootheme) (`25` built-in dark/light/circadian presets, `34` semantic color tokens, `NO_COLOR=1`, and `--json`) and exposes `<binary> about` (`ooda about catalog`).
- **Tags**: `#openooda` `#capability-security` `#zero-trust` `#deterministic` `#post-quantum-cryptography` `#cisa-kev` `#package-manager` `#catalog` `#sha256` `#minisign` `#supply-chain-security`

## Module Anatomy (`135` `.oo` Pages — Power-of-2 Shape Ladder `1/2/4/8/16/32/64/128/256`)

| Page | Role & Logline |
| :--- | :--- |
| [`.github/anchor.oo`](.github/anchor.oo) | GitHub auto-release and Pages deploy. Not product code. |
| [`.github/workflows/anchor.oo`](.github/workflows/anchor.oo) | File-tree gate, auto-release on push to main, Pages deploy. |
| [`OS/oomodemd/anchor.oo`](OS/oomodemd/anchor.oo) | Stock catalog package for oomodemd. |
| [`OS/oomodemd/oomodemd.oo`](OS/oomodemd/oomodemd.oo) | Cellular 5G/LTE baseband and eSIM isolation daemon. |
| [`anchor.oo`](anchor.oo) | The list of packages opm search and opm add can install. |
| [`apps/ooarcade/anchor.oo`](apps/ooarcade/anchor.oo) | Stock catalog package for ooarcade. |
| [`apps/ooarcade/ooarcade.oo`](apps/ooarcade/ooarcade.oo) | Original 2D/2.5D action platformer/metroidvania + rollback fighting suite |
| [`apps/oocamera/anchor.oo`](apps/oocamera/anchor.oo) | Stock catalog package for oocamera. |
| [`apps/oocamera/oocamera.oo`](apps/oocamera/oocamera.oo) | Capability-gated camera and ISP application. |
| [`apps/oocommand/anchor.oo`](apps/oocommand/anchor.oo) | Stock catalog package for oocommand. |
| [`apps/oocommand/oocommand.oo`](apps/oocommand/oocommand.oo) | Original real-time strategy suite with deterministic sim core |
| [`apps/ooemu/anchor.oo`](apps/ooemu/anchor.oo) | Stock catalog package for ooemu. |
| [`apps/ooemu/ooemu.oo`](apps/ooemu/ooemu.oo) | Multi-core emulator core with cycle-accurate scheduling and state snapshots |
| [`apps/oostrike/anchor.oo`](apps/oostrike/anchor.oo) | Stock catalog package for oostrike. |
| [`apps/oostrike/oostrike.oo`](apps/oostrike/oostrike.oo) | Original 6-DoF space combat simulator with orbital mechanics |
| [`apps/oovoxel/anchor.oo`](apps/oovoxel/anchor.oo) | Stock catalog package for oovoxel. |
| [`apps/oovoxel/oovoxel.oo`](apps/oovoxel/oovoxel.oo) | Original voxel sandbox with chunked terrain and redstone-style logic |
| [`caps/anchor.oo`](caps/anchor.oo) | Stock catalog package that prints the 20 language capability tokens. |
| [`caps/caps.oo`](caps/caps.oo) | Print all 32 canonical openOODA explicit capabilities (19 software/OS + 13 hardware). |
| [`core/ooda/anchor.oo`](core/ooda/anchor.oo) | Stock catalog package for ooda, the canonical L0 flagship CLI. |
| [`core/ooda/ooda.oo`](core/ooda/ooda.oo) | Canonical openOODA developer driver and command router for build, run, test, fmt, install, qa, fix, and about. |
| [`docs/anchor.oo`](docs/anchor.oo) | Index of the user-facing docs for the public catalog. |
| [`echo/anchor.oo`](echo/anchor.oo) | Stock catalog package that prints echo. Safe to launch. |
| [`echo/echo.oo`](echo/echo.oo) | Print echo. A second package for the openOODA catalog. |
| [`examples/anchor.oo`](examples/anchor.oo) | Walkthroughs that fetch a shelf part and try it. |
| [`hello/anchor.oo`](hello/anchor.oo) | Stock catalog package that prints hello. Safe to launch. |
| [`hello/hello.oo`](hello/hello.oo) | Print hello. A first package for the openOODA catalog. |
| [`ooarp/anchor.oo`](ooarp/anchor.oo) | Stock catalog package for ooarp. |
| [`ooarp/ooarp.oo`](ooarp/ooarp.oo) | Inspects and flushes neighbor discovery and ARP tables on local network segments. |
| [`oodig/anchor.oo`](oodig/anchor.oo) | Stock catalog package for oodig. |
| [`oodig/oodig.oo`](oodig/oodig.oo) | Comprehensive DNS lookup utility querying specific record types (A, AAAA, MX, TXT). |
| [`oodns/anchor.oo`](oodns/anchor.oo) | Stock catalog package for oodns. |
| [`oodns/oodns.oo`](oodns/oodns.oo) | Asynchronous DNS resolver supporting DNS-over-HTTPS and capability allowlists. |
| [`oohost/anchor.oo`](oohost/anchor.oo) | Stock catalog package for oohost. |
| [`oohost/oohost.oo`](oohost/oohost.oo) | Quick DNS address resolver performing forward and reverse host conversions. |
| [`ooping/anchor.oo`](ooping/anchor.oo) | Stock catalog package for ooping. |
| *... (+99 additional `.oo` pages)* | Bounded under the Power-of-2 directory and page laws (`<= 256` lines/page) |

## Build, Deterministic Verification & 8-Hat Consensus Gates

```sh
make build                                         # Compile native ELF binary via oodac
make test                                          # Run functional /tmp round-trip + negative-trust refusal tests
make det                                           # Diverse Double-Compilation bit-for-bit determinism gate
/Projects/openOODA-agents/oohat/bin/oohat cycle .  # 8-Hat consensus + CISA KEV gate (quorum_mask=255)
```
