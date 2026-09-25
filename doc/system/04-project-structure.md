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
