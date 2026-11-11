---
id: "FEAT-2"
priority: "Must have"
area: "Fleet"
sprint: "Sprint 2"
december: "In (kart grid and the kart page, for every kart)"
tags: [feature]
updated: 2026-11-06
---
# Kart service history

Back to [Features](Features.md)

## User story

As a mechanic, I see a kart's status, open issues and past repairs before I start, and I log what I did when I finish.

## What it includes

- A grid of all karts at the Brussels venue with number, photo, status and open issues. The status uses Supercube's four values (Good, Diagnostic, Broken, Permanently broken), shown with a word and a colour.
- The kart page lists open issues, past repairs and (later) machine alerts, newest first, with date, person, parts and photos.
- Logging a repair uses quick picks and voice; parts taken are filled in; an open issue can be closed with an optional "after" photo; the kart can be marked repaired in the same flow.
- The history is one query over service events, issues and alerts; nothing is copied.
- A venue field is kept so more venues can be added later.

## Planning

- **Sprint:** Sprint 2 (Must have).
- **December prototype:** In (kart grid and the kart page, for every kart).
- **Requirements:** FR-30, FR-31; US-13, US-14, US-20 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[Supercube kart status and diagnostics](Supercube%20kart%20status%20and%20diagnostics.md), [Photo issues (camera)](Photo%20issues%20%28camera%29.md), [Repair notes with senior approval](Repair%20notes%20with%20senior%20approval.md)
