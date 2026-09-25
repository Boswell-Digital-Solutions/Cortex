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
