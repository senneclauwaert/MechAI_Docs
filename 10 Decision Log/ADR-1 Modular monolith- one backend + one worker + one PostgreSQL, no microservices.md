---
id: "ADR-1"
area: "Architecture"
status: "Accepted"
date: "2026-10-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-1 Modular monolith: one backend + one worker + one PostgreSQL, no microservices

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** The first plan had seven microservices, each with its own database, plus an event bus and an API gateway. The grade needs a full analysis and a working prototype, not microservices, and the team is two people.

**Decision:** One backend program split into modules with strict borders, plus one background worker, with one PostgreSQL database (one schema per module). No message broker and no API gateway. Confirmed on 10 October and again on 6 November 2026.

**Why:** One deployable is faster to build, cheaper to run and easier to explain. Seven services would mean seven Dockerfiles, pipelines, migrations and health checks. The module borders show where the app could be split later.

**Alternatives considered:** Seven microservices with an event bus and a gateway; three services.

**Consequences:** Modules talk through `service.py` function calls and small in-process events, never through each other's tables. If events must ever be reliable, the outbox pattern can be added.
