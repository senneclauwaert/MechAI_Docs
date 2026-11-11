---
id: "ADR-12"
area: "Security"
status: "Accepted"
date: "2026-10-16"
tags: [decision]
updated: 2026-11-06
---
# ADR-12 No accounts: profile picker + personal PIN, 30-minute idle logout

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · amended 6 Nov 2026

**Context:** Workshop tablets are shared and used with gloves. Email accounts and passwords would slow everyone down.

**Decision:** A start screen lists the profiles; a person taps their name and enters their own PIN (4 to 6 digits, stored as an Argon2 hash). 5 wrong tries lock the profile; PIN attempts are rate limited. Logout after 30 minutes without activity. No outside login service and no device setup code: MechAi is only reachable on Supercube's internal network (6 November 2026).

**Why:** Fast, simple and enough for an internal tool; every action is still tied to a person.

**Alternatives considered:** Microsoft Entra External ID; Cloudflare Access; a device setup code per tablet.

**Consequences:** All login code lives in the `auth` module, so Supercube can put its own login in front later. Roles are in [ADR-26 Four roles- operator, mechanic, senior mechanic, admin](ADR-26%20Four%20roles-%20operator,%20mechanic,%20senior%20mechanic,%20admin.md).
