# Cortex (Desktop) — Compiled System Reference

**Designation:** cxd
**Document role:** Canonical compiled technical reference for this standalone Cortex desktop app
**Source:** `doc/system/`
**Build command:** `bash doc/system/BUILD.sh`
**Document version:** 1.0 (2026-09-24) — initial doc/system authored from scratch
**Protocol:** BDS Documentation Protocol v2.0

> **Generated artifact warning:** `doc/cxdSYSTEM.md` is assembled output.
> Edit the source modules under `doc/system/` and rebuild. Hand edits to
> generated artifacts are overwritten by the next build.

**Not the bds/Forge Cortex family:** this repo shares the name "Cortex"
with `cortex_bds` and `forge-cortex` by coincidence only — it is unrelated
to that family. See `01-overview-philosophy.md`. The designation `cxd`
("Cortex Desktop") was deliberately chosen instead of anything
`cor`/`cbd`/`fcx`-adjacent to avoid compounding the naming collision.

This `doc/system/` tree is the canonical source of truth for this repo. It
uses explicit **truth classes**: canonical facts define role, architecture,
and authority boundaries; snapshot facts are dated, audit-derived
observations (versions, performance figures) that must be re-measured
before reuse.

Assembly contract:

- Command: `bash doc/system/BUILD.sh`
- Validation: `bash doc/system/validate_snapshots.sh` runs during assembly
- Primary output: `doc/cxdSYSTEM.md`

| Part | File | Contents |
| --- | --- | --- |
| §1 | `01-overview-philosophy.md` | Purpose and the Cortex-naming collision disclaimer |
| §2 | `02-architecture.md` | Tauri/Rust backend + SvelteKit frontend split |
| §3 | `03-tech-stack.md` | Stack details |
| §4 | `04-project-structure.md` | Directory layout |
| §5 | `05-config-env.md` | Configuration (currently none found) |
| §6 | `06-testing.md` | Test commands |
| §7 | `90-handover.md` | Maturity note and pointers to this repo's own extensive status docs |

## Quick Assembly

```bash
bash doc/system/BUILD.sh
```
