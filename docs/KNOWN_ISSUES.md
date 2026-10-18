# Known Issues



## 2026-10-18 — Documentation check-mode limit

**Status: OPEN verification limit.** `doc/system/BUILD.sh` does not parse
`--check`; that invocation rebuilds the output and returns success. This change
uses before/after generated-output hashes to check deterministic rebuilds. It
does not claim a strict stale-document guard. The existing builder was not
changed as part of Debian package inspection.
