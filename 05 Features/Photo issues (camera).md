---
id: "FEAT-12"
priority: "Must have"
area: "Issues"
sprint: "Sprint 2 (reporting), sprint 3 (to-do and alert)"
december: "In (issue reporting by the operator); stretch goal (photos, to-do and alert)"
tags: [feature]
updated: 2026-11-06
---
# Photo issues (camera)

Back to [Features](Features.md)

## User story

As an operator or mechanic, I report a problem on a kart with a quick reason, an optional spoken description and photos. It shows in the kart history, can become a to-do, and alerts the senior mechanics when the kart is unsafe.

## What it includes

- "Report issue": tap the kart, pick a reason (noise, steering, brakes, battery, damage, other), optionally speak a sentence and take photos (at most 6), pick a severity: low, high or kart unsafe.
- The operator can mark the kart broken in the same flow.
- One Issue record with the status open, in progress or fixed. The kart history, to-dos and alerts point to that record.
- One tap turns the issue into a to-do; closing it marks the issue fixed, with an optional "after" photo.
- "Kart unsafe" marks the kart broken and alerts the senior mechanics.
- Photos are resized on the device and on the server, stored on the `files` volume and served only after sign-in.
- Rule: do not photograph people.

## Planning

- **Sprint:** Sprint 2 (reporting), sprint 3 (to-do and alert) (Must have).
- **December prototype:** in (issue reporting by the operator); stretch goal (photos, to-do and alert).
- **Requirements:** FR-40, FR-41; US-12, US-21 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[ADR-14 Photo issues- one Issue record linked to history, to-dos and alerts](../10%20Decision%20Log/ADR-14%20Photo%20issues-%20one%20Issue%20record%20linked%20to%20history,%20to-dos%20and%20alerts.md), [ADR-28 Files on a Docker volume behind one storage module](../10%20Decision%20Log/ADR-28%20Files%20on%20a%20Docker%20volume%20behind%20one%20storage%20module.md), [Data model](../03%20Architecture/Data%20model.md)
