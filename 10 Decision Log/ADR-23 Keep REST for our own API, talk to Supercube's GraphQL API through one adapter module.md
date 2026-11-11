---
id: "ADR-23"
area: "Architecture"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-23 Keep REST for our own API; talk to Supercube's GraphQL API through one adapter module

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · amended 6 Nov 2026

**Context:** Supercube shared its GraphQL schema. It offers live kart (pod) status, alerts, status changes and diagnostics.

**Decision:** MechAi keeps REST for its own API. One module, `supercube`, is a GraphQL client of Supercube's API. It reads status and alerts, marks karts broken or repaired, and starts and stops diagnostics (Pitlane, Cruise, Boost, High boost, High brake) with no extra PIN, like Supercube's operator app. Every action is logged. MechAi uses Supercube's four kart statuses. A fake client is used until access is granted.

**Why:** REST fits our forms, uploads and assistant call. Talking to Supercube through one module means a schema change touches only that module. Mirroring the operator app keeps the workflow familiar.

**Alternatives considered:** Rewriting our API in GraphQL; read-only integration; never starting diagnostics from MechAi.

**Consequences:** The real connection needs Supercube's written OK and credentials. See [Supercube integration (GraphQL)](../03%20Architecture/Supercube%20integration%20%28GraphQL%29.md).
