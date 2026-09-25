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
