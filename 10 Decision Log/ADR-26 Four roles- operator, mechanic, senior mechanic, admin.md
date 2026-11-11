---
id: "ADR-26"
area: "Security"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-26 Four roles: operator, mechanic, senior mechanic, admin

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** The operator, who receives customers and runs sessions, is often the first to notice a kart problem.

**Decision:** Four roles. **Operator:** report issues with a photo, see kart status, mark a kart broken. **Mechanic:** assistant, history, stock, repairs, kart status, diagnostics. **Senior mechanic:** mechanic plus approving repair notes and unsafe-issue alerts. **Admin:** users, parts, karts and handbook uploads. The backend checks the role on every request.

**Why:** Problems are logged where they are noticed; each role sees only what it needs.

**Alternatives considered:** Three roles without the operator.

**Consequences:** The operator's exact rights are an assumption to confirm with Supercube.
