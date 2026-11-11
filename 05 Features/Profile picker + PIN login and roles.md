---
id: "FEAT-8"
priority: "Must have"
area: "Auth"
sprint: "Sprint 1"
december: "In (all four roles)"
tags: [feature]
updated: 2026-11-06
---
# Profile picker + PIN login and roles

Back to [Features](Features.md)

## User story

As a user of a shared workshop tablet, I tap my name and enter my own PIN; after 30 minutes without activity I am logged out. Each role sees only its own actions.

## What it includes

- The start screen ("Who is working?") shows every profile with name, photo and role.
- Each person chooses a PIN of 4 to 6 digits at first use; it is stored only as an Argon2 hash.
- After 5 wrong PINs the profile is locked for 5 minutes; an admin can unlock it earlier and reset the PIN. PIN attempts are rate limited per device.
- After 30 minutes without activity the session ends. A "Switch user" button is always visible.
- Four roles: **operator** (report issues, see status, mark a kart broken), **mechanic** (assistant, history, stock, repairs, status, diagnostics), **senior mechanic** (mechanic plus approving notes and unsafe-issue alerts), **admin** (users, parts, karts, handbook uploads).
- The backend checks the role on every request. Every action is written to the audit log.
- No device setup code: MechAi is only reachable on Supercube's internal network.
- All login code lives in the `auth` module, so Supercube can put its own login in front later.

## Planning

- **Sprint:** Sprint 1 (Must have).
- **December prototype:** In (all four roles).
- **Requirements:** FR-50, FR-51; US-01, US-02 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[ADR-12 No accounts- profile picker + personal PIN, 30-minute idle logout](../10%20Decision%20Log/ADR-12%20No%20accounts-%20profile%20picker%20+%20personal%20PIN,%2030-minute%20idle%20logout.md), [ADR-26 Four roles- operator, mechanic, senior mechanic, admin](../10%20Decision%20Log/ADR-26%20Four%20roles-%20operator,%20mechanic,%20senior%20mechanic,%20admin.md), [Architecture](../03%20Architecture/Architecture.md)
