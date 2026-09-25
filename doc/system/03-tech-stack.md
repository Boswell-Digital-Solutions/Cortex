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
