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
