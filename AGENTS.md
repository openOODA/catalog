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

---

## 7. Multi-Engine Audit Protocol (Pre-Release)

Advisory tiered audit run before tagging releases, budgeted by token capacity:
1. **`mcode`** (Abundant tokens): Full codebase scan for contract mismatches, packaging specs, and CI gates.  
   `mcode exec --permission full "<prompt>"`
2. **`vibe`** (Moderate tokens): Adversarial diff inspection for subtle regressions, security bypasses, and API validity.  
   `vibe -p "<prompt>" --trust --auto-approve`
3. **`grok`** (Strict quota): High-value referee and final sanity check on critical release diffs.  
   `grok -p "<prompt>" --always-approve`

**Rule:** External audits are strictly advisory; all findings must be verified against source code. External LLMs never gate CI—the §5 Verification Ladder is the sole canonical authority.
