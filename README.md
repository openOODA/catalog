<div align="center">

<pre>
   ____  ____  ___  ____    ___   ___  ____    _
  / __ \/ __ \/ _ \/ __ \  / _ \ / _ \|  _ \  / \
 / /_/ / /_/ /  __/ / / / | | | | | | | | | |/ _ \
/_____/ .___/\___/_/ /_/  | |_| | |_| | |_| / ___ \
      /_/                   \___/ \___/|____/_/   \_\
</pre>

### `catalog` — Cryptographically Signed Public Package Catalog & `@group` Index (`L0`–`L7`)

[openooda.org](https://openooda.org) • [`openOODA/catalog`](https://github.com/openOODA/catalog) • [Public Binary Hub (`install@hub`)](https://github.com/openOODA/install/releases/tag/hub) • [Governance & Quick Cards (`openOODA/openOODA`)](https://github.com/openOODA/openOODA)

</div>

---

## Overview

**`openOODA/catalog`** is the cryptographically signed public package catalog and Fedora-style `@group` registry for all **93 canonical packages** across `L0`–`L7`. Every package manifest declares its explicit `CapReg64` (`0..31`) capability requirements ahead of installation.

## Directory Layout (Option A — `layers/L0-core` .. `layers/L7-agents`)

All 8 layers live inside [`layers/`](layers/) with `L0-` .. `L7-` prefixes so GitHub and `ls` sort them in exact architectural order (`L0` -> `L7`), while packages inside each layer sort alphabetically:

```text
openOODA/catalog/
├── layers/                            # Exact 8 (2^3) layer directories, sorted L0 -> L7:
│   ├── L0-core/                       # 7 packages (ooda, oodac, oodar, oolsp, oomcp, oopm, oostd)
│   ├── L1-kernel/                     # 6 packages (ooboot, oodrv-io, oodrv-storage, oodrv-virt, oohal, ookernel)
│   ├── L2-OS/                         # 9 packages (ooauthd, oocontainer, oohealthd, ooinit, oollama, oomodemd, oonetd, oosysbus, oovfs)
│   ├── L3-tools/                      # 39 packages (ooarchive, ooawk, oocat, oodefense, oosandbox, ootheme, ooui, ooengine, ...)
│   ├── L4-DE/                         # 8 packages (ooagent-hud, oobazaar, oocomp, oofiles, oopanel, ooportal, oosettings, ooterm)
│   ├── L5-apps/                       # 16 packages (oomedia, oodaw, oocanvas, oooffice, ooflash, oobrowser, oostudio, + 5 games, ...)
│   ├── L6-cloud/                      # 8 packages (oobilling, oodb, oodeploy, oogateway, ooidentity, oomesh, oostore, ootelemetry)
│   └── L7-agents/                     # 10 packages (oobench, oocode, ooconsensus, oofalsify, oogovern, oohat, ooloop, oomemory, ooquota, ooswarm)
├── groups.oot                         # Fedora-style @group profiles (@core, @kernel, @os, @tools, @de, @apps, @games, @cloud, @agents, @all)
├── catalog                            # Master pipe-delimited index (<pkg>|<version>|<caps>|<deps>|<sha256>)
├── index                              # Signed index mirror served at https://catalog.openooda.org/index
├── index.sig / index.minisig          # HMAC-SHA256 & Minisign cryptographic signatures over index
├── registry.pub                       # Public verification key for index.minisig
├── SHA256SUMS                         # Master SHA-256 digests for all assets in openOODA/install@hub
├── docs/                              # Catalog format & signing documentation (.oot)
├── qa/                                # Pure .oo catalog verifier & signer (catalog_proof.oo, check_pkg.oo, sign_index.oo)
└── tests/                             # Pure .oo 97-assertion verification suite (test_catalog.oo)
```

## Quick Usage (`oopm`)

```sh
oopm group list                  # List @core, @kernel, @os, @tools, @de, @apps, @games, @cloud, @agents, @all
oopm search oomedia              # Inspect package version, layer, and required CapReg64 capabilities
oopm install @core               # Install the L0 core toolchain
oopm install @all                # Install all 93 canonical packages
```
