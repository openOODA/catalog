# catalog: Agent Engineering Standards (v1)

This repository houses the public package registry and metadata catalog for openOODA (`opm search`).
All work in this repository strictly defers to the organization standards in [`openOODA/AGENTS.md`](file:///home/ubermetroid/Projects/openOODA/openOODA/AGENTS.md).

---

## 1. Catalog Architecture & Invariants
- **Curated Packages**: Manifests declare unforgeable author identity, package versions, and capability declarations.
- **Cryptographic Proofs**: Minisign and SHA-256 verification of listed packages.
- **Index Integrity**: Every entry in the catalog file links to a valid manifest.

---

## 2. Invariants & Quality Standards
- **The Page Rule**: Every `.oo` verification page must be between 16 and 256 lines.
- **Directory Density**: At most 8 `.oo` pages per directory.
- **Double-Run Determinism**: All `qa/*_proof.oo` suites must pass sequentially in fresh processes.

---

## 3. Local Verification Commands
```bash
cli check qa/anchor.oo
cli qa
```
