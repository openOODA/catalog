# Agent Instructions for catalog

You are operating within the openOODA polyrepo. The catalog repo
is the **public package list** hosted at `https://catalog.openooda.org`.
It is the source of truth for the 4 stock packages (caps, echo,
hello, sqlite) and the signing key (`registry.pub`) that opm uses
to verify the minisig on every HTTPS-fetched payload. Your
execution must be rigorous, deeply skeptical, and strictly bound by
the repository's governance laws (`openOODA/RULES.oot` and
`openOODA/FLOOR.oot`).

## 1. Zero Trust & The Double-Run Law
- **The catalog is the SSoT for stock.** `opm/seed/catalog` is
  a local mirror; `catalog/catalog` (this repo) is the public
  source. Any drift between them is a real defect — see the
  2026-09-10 focused audit for the cross-repo drift pattern.
- **SHAs must match exactly.** `opm/seed/caps/caps.oo` and
  `catalog/caps/caps.oo` must have the same sha256. If they
  diverge, opm will reject the HTTPS add (minisig verify fails).
- **4 stock packages, no more, no less.** The 4 are caps
  (20 capability tokens), echo (print demo), hello (print demo),
  sqlite (boundary adapter demo). Adding a 5th requires a new
  minisig + a new commit; do not add new stock packages
  unilaterally.
- **Minisig verification is the integrity boundary.** The
  `index.minisig` is the public-key signature over `index`. The
  private key is held by the catalog maintainer. Do not commit
  the private key to any repo.

## 2. Services for Speed (No Shortcuts)
- **Do not blindly `grep` the tree.** Use the catalog binary
  itself where possible (this repo is mostly static files; the
  binary is in opm).
- **The 4 stock package folders** (the canonical surface):
  - `caps/` — 20 capability tokens (anchor: ANCHOR.oo beat 1).
  - `echo/` — print demo (anchor: ANCHOR.oo beat 2).
  - `hello/` — print demo (anchor: ANCHOR.oo beat 2).
  - `sqlite/` — boundary adapter demo (anchor: ANCHOR.oo beat 3c).
- **The catalog index file (`catalog`)** is a 4-line pipe-delimited
  text file: `name|version|caps|deps|sha`. Rebuild it with
  `opm bot .` from the opm repo (or manually per the manifest
  convention).
- **The minisig chain:** `index` (the data) is signed by
  `index.sig` (the signature) and stored as `index.minisig`
  (the human-readable form). Verify with
  `qa/sign_index.oo`. Do not bypass the chain.

## 3. Strict Repository Compliance
- **No VERSION file.** The tag IS the version (RFC-0006).
  Current tag: `v0.0.13`.
- **Pure Files:** Only `.oo`, `.oot`, `.md`, `.yml` files are
  permitted for logic (RULES.oot §1.14). No `*.sh`, `*.py`,
  etc. in the product tree.
- **Line Limits:** Absolute maximum of 256 lines per file. The
  `qa/catalog_proof.oo` is at 252/256 (4 lines headroom); defer
  split until an addition is planned.
- **Per-package ANCHOR.oo pattern:** each stock package folder
  has a 4-element Academy header (Logline, Setup, Beats). This
  pattern was established in commit `52d94b7` (sqlite bridge) and
  is the convention for all new stock packages.
- **Public hosting:** the `CNAME` file pins
  `catalog.openooda.org`. The `.nojekyll` prevents GitHub Pages
  from running the manifests through a Jekyll build. Do not
  delete either.

## 4. Commit Hygiene
- **One Repo, One Commit:** Never bundle changes across multiple
  repositories in a single commit (FLOOR.oot §10).
- **Minisig Rotation:** rotating the minisig key is a
  multi-repo operation (catalog, opm, oodar, std). Bump the
  `registry.pub` here and the corresponding
  `cli/registry.pub` in opm/ in the same release window.
- **Adding a stock package:** a single same-commit patch that
  updates `catalog/`, `index`, `index.minisig`, AND
  `audit/ANCHOR.oo` (the curated-audit index). Bump the tag when
  the 5th package lands.
- **Tag = VERSION:** This repo has no VERSION file. The tag IS
  the version (RFC-0006).
