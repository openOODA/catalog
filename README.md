<div align="center">

<pre>
   ____  ____  ___  ____    ___   ___  ____    _
  / __ \/ __ \/ _ \/ __ \  / _ \ / _ \|  _ \  / \
 / /_/ / /_/ /  __/ / / / | | | | | | | | | |/ _ \
/_____/ .___/\___/_/ /_/  | |_| | |_| | |_| / ___ \
      /_/                   \___/ \___/|____/_/   \_\
</pre>

### openOODA — Sovereign Systems Language for the AI Era

[openooda.org](https://openooda.org)

</div>

---

## This repo: catalog

The public list of openOODA packages. `opm search` reads the `catalog` file. `opm add` installs a child folder (manifest plus `.oo` payload). This is a file tree, not a registry service.

Host: `https://catalog.openooda.org`

## Use

```sh
opm search hello
opm add hello
```

From this tree, opm also reads `seed/` inside the opm repo so search works with no network. This catalog repo is the copy the world can fetch.

## Add a package

1. Add a folder with `manifest` and a `.oo` payload (Academy headers required).
2. From the opm repo, run `opm bot` with this tree as the target to rebuild `catalog`.
3. Sign `catalog` to `index.minisig` with the catalog minisign key.
4. Commit the folder, `catalog`, `index`, and `index.minisig`.

## Docs

All design, RFCs, practices, and onboarding live in [openOODA/openOODA](https://github.com/openOODA/openOODA) or at [openooda.org](https://openooda.org).

## The Polyrepo

| Repo | Purpose |
|------|---------|
| [openOODA/openOODA](https://github.com/openOODA/openOODA) | Governance, RFCs, laws |
| [openOODA/oodar](https://github.com/openOODA/oodar) | Runtime substrate |
| [openOODA/oodac](https://github.com/openOODA/oodac) | Compiler |
| [openOODA/std](https://github.com/openOODA/std) | Standard library |
| [openOODA/ooda](https://github.com/openOODA/ooda) | `ooda` workflow driver |
| [openOODA/install](https://github.com/openOODA/install) | How the toolchain lands (install.sh, apt, dnf, pacman) |
| [openOODA/opm](https://github.com/openOODA/opm) | Package manager |
| [openOODA/catalog](https://github.com/openOODA/catalog) | Public package catalog |
| [openOODA/lsp](https://github.com/openOODA/lsp) | Language server |
| [openOODA/mcp](https://github.com/openOODA/mcp) | MCP server |
| [openOODA/blackbox](https://github.com/openOODA/blackbox) | Operational Logistics: Agent-native execution flight recorder and crash autopsy engine |
| [openOODA/website](https://github.com/openOODA/website) | Website source |
| [openOODA/.github](https://github.com/openOODA/.github) | Org profile, shared community files, workflows |

## License

Dual-licensed under your choice of MIT or Apache 2.0. See [LICENSE](LICENSE)
for full text and the canonical URLs.
