---
id: "FEAT-14"
priority: "Must have"
area: "Supercube"
sprint: "Sprint 2 (status), sprint 3 (diagnostics)"
december: "Kart status inside MechAi is in; sending it to Supercube and diagnostics are a stretch goal with the fake client"
tags: [feature]
updated: 2026-11-06
---
# Supercube kart status and diagnostics

Back to [Features](Features.md)

## User story

As an operator or mechanic, I mark a kart broken or repaired in MechAi, and Supercube's system shows it at once. As a mechanic, I run diagnostics the same way as in Supercube's operator app.

## What it includes

- **Mark broken** (operator, mechanic, senior, admin) and **mark repaired** (mechanic, senior, admin) call Supercube's `podBroken` and `podRepaired`.
- **Diagnostics:** tap Diagnostics, then Pitlane, Cruise, Boost, High boost or High brake; a big Stop button ends it. No extra PIN, like the operator app.
- Every action is logged with the person and time.
- If Supercube refuses or cannot be reached, the user sees a `SUPERCUBE_` error code and the local status does not change.
- The worker keeps the kart status and alerts in sync.
- A fake client with demo data is used until Supercube grants API access.

## Planning

- **Sprint:** Sprint 2 (status), sprint 3 (diagnostics) (Must have).
- **December prototype:** kart status inside MechAi is in; sending it to Supercube and diagnostics are a stretch goal with the fake client.
- **Requirements:** FR-32 to FR-34; US-15, US-16 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[Supercube integration (GraphQL)](../03%20Architecture/Supercube%20integration%20%28GraphQL%29.md), [ADR-23 Keep REST for our own API, talk to Supercube's GraphQL API through one adapter module](../10%20Decision%20Log/ADR-23%20Keep%20REST%20for%20our%20own%20API,%20talk%20to%20Supercube's%20GraphQL%20API%20through%20one%20adapter%20module.md)
