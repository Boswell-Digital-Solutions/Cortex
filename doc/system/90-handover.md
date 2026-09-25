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
