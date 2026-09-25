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

---

# Overview and Philosophy

Cortex is a desktop application that indexes local files and provides
full-text search over them, plus a feature to export indexed content in a
format suited for pasting into AI coding-assistant conversations (branded in
this repo as "VS Code Claude Export").

**Canonical fact:** Cortex is offline-first. Indexed content and the search
index live in a local SQLite database; there is no cloud component and no
telemetry described anywhere in this repo's own documentation.

**Canonical fact — naming collision, read this first:** this repository is
**not** related to `cortex_bds` (`ecosystem/local-systems/cortex_bds`) or
`forge-cortex` (`apps/public-app-local-support/forge-cortex`), despite
sharing the name "Cortex." Those two are bds/Forge-family local
file-intelligence services built to a shared constitutional-doctrine
pattern (`PROJECT_CHARTER.md`, `LOCAL_DOCTRINE.md`,
`AUTHORITY_BOUNDARIES.md`). This repository predates and is unrelated to
that family: it is a standalone desktop app with its own Tauri/Rust/SQLite
stack and no shared doctrine files. Confirm the repository path before
treating any architectural claim about "Cortex" as applying to this repo
versus one of the other two.

**Snapshot fact:** the repository's own `package.json`/README badges report
version `0.1.0-alpha` at the time this chapter was written. Treat this as a
point-in-time observation, not a current-truth claim — re-check the actual
version file before relying on it.

---

# Architecture

Cortex is a Tauri 2.0 desktop application: a Rust backend (`src-tauri/`)
paired with a SvelteKit frontend (`src/`), communicating over Tauri's IPC
command layer rather than HTTP.

**Canonical fact:** the Rust backend is organized into these modules under
`src-tauri/src/`: `indexer` (walks and indexes local files), `search`
(queries the index), `db` (SQLite access), `export` (the VS Code/Claude
export feature), `ai` (AI-related functionality), `commands` (the Tauri
`#[tauri::command]` surface the frontend calls), plus `state.rs` (shared
application state) and `error.rs` (error types).

**Canonical fact:** search is implemented over SQLite FTS5 (full-text
search), per the README's stated sub-100ms query target — this is a design
target as stated by the repo's own README, not independently re-verified
while authoring this chapter.

**Canonical fact:** the frontend (`src/routes/`, `src/lib/`) is a SvelteKit
application that talks to the Rust backend exclusively through Tauri
commands; it is not a general web app and has no independent HTTP backend
of its own.

**Not yet established here:** the exact boundary between the `ai` and
`export` modules, and whether the "AI Q&A"-style feature set described
elsewhere in this repo's status documents is implemented, partially
implemented, or only planned. Do not assume feature-complete status for
anything not confirmed directly in code.

---

# Tech Stack

**Canonical fact — backend:**

- Rust (README states 1.75+)
- Tauri 2.0 (desktop application shell and IPC)
- SQLite with FTS5 (embedded database and full-text search)

**Canonical fact — frontend:**

- SvelteKit
- Svelte 5
- TypeScript
- Tailwind CSS

**Canonical fact:** this is a desktop-only application distributed via
Tauri's native packaging (the README states Linux, macOS, and Windows
support); it has no server deployment target.

---

# Project Structure

```text
src-tauri/          Rust backend (Tauri)
  src/
    ai/            AI-related functionality
    commands/      Tauri #[tauri::command] surface called by the frontend
    db/            SQLite access
    export/        VS Code / Claude export feature
    indexer/       File-walking and indexing
    search/        FTS5 query layer
    state.rs       Shared application state
    error.rs       Error types
    lib.rs, main.rs
  tests/           Backend test suite (see tests/README.md)
src/               SvelteKit frontend
  routes/          SvelteKit pages
  lib/             Shared frontend code
  app.html, app.css
docs/              Developer-facing guides (DEVELOPER_GUIDE.md, API_REFERENCE.md,
                   USER_GUIDE.md, CONTRIBUTING.md, DEPLOYMENT.md)
DOCUMENTATION.md   Index into the many top-level status/summary/guide files
```

**Canonical fact:** `DOCUMENTATION.md` at the repo root is this repo's own
navigation index into a large number of top-level status and summary files
(phase summaries, session summaries, due-diligence reports). This
`doc/system/` tree does not attempt to re-index all of those — see
`DOCUMENTATION.md` directly for that inventory.

---

# Configuration and Environment

**Canonical fact:** no `.env` file or environment-variable-based
configuration was found anywhere in this repository while authoring this
chapter, and no API key or external-service credential usage was found in
the `ai` module specifically. Cortex, as currently implemented, appears to
require no external configuration to run — all state is local (SQLite).

**Not yet established here:** whether this is a deliberate design choice
(fully local, no external calls) or whether external-AI functionality is
planned but not yet implemented. See `02-architecture.md`'s open question
about the `ai` module's actual scope.

---

# Testing

**Canonical fact:** backend tests run via Cargo, from `src-tauri/`:

```bash
cargo test --lib
cargo test --test integration_test
```

See `src-tauri/tests/README.md` and `TESTING.md` at the repo root for the
fuller test-suite guide, including a `db_benchmark` binary
(`cargo run --bin db_benchmark --release`) for database performance
measurement.

**Snapshot fact:** this chapter does not restate any specific pass/fail
count or coverage percentage from this repo's own status files —
those are dated, audit-derived numbers that belong in that status file
directly and would go stale immediately if duplicated here.

---

# Handover

**Canonical fact:** this repository carries an unusually large number of
top-level status, summary, and phase-report markdown files (phase
summaries, session summaries (`CX-###-SUMMARY.md`), a due-diligence report,
implementation-complete reports). `DOCUMENTATION.md` is this repo's own
index into them. This `doc/system/` tree does not attempt to reconcile or
summarize their content — treat each one as a dated, point-in-time record,
not current truth, unless independently re-verified.

**Known limitation of this chapter set:** it was authored from the repo's
README, `DOCUMENTATION.md`, `docs/DEVELOPER_GUIDE.md`, and a direct read of
`src-tauri/src/`'s module layout — not from a full audit of every status
file or a runtime verification of every claimed feature. Treat feature
claims (e.g. "50+ files/second," "sub-100ms search") as the repo's own
stated targets, not independently confirmed facts.

**Operator note:** before adding features to the `ai` or `export` modules,
read `docs/API_REFERENCE.md` and `docs/DEVELOPER_GUIDE.md` directly — this
chapter set does not duplicate their content.
