---
id: "ADR-15"
area: "Process"
status: "Accepted"
date: "2026-10-24"
tags: [decision]
updated: 2026-11-06
---
# ADR-15 Simple, readable code with one copy-paste module template

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · amended 6 Nov 2026

**Context:** Two students must build, explain and maintain the code, and Supercube may keep it (ownership, licence and maintenance are still open; see [Open questions](../01%20Project/Open%20questions.md)).

**Decision:** Every module has the same files (`models.py`, `schemas.py`, `service.py`, `router.py`, `errors.py`, README). Code is modular, readable, not duplicated and cleanly formatted. ruff (Python) and Prettier and ESLint (TypeScript) enforce the formatting through pre-commit and CI (added 6 November 2026).

**Why:** A new feature is copy, rename and change; any reviewer can follow an endpoint in a minute; formatting is never a discussion.

**Alternatives considered:** Free structure per feature; layered architecture with repositories and interfaces.

**Consequences:** See the module template in [Architecture](../03%20Architecture/Architecture.md).
