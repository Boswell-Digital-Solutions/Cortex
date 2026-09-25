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
