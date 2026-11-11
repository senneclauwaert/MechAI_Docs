---
id: "FEAT-1"
priority: "Must have"
area: "Inventory"
sprint: "Sprint 3"
december: "In (part lookup and taking a part)"
tags: [feature]
updated: 2026-11-06
---
# Inventory management

Back to [Features](Features.md)

## User story

As a mechanic, I search or pick a part from the list to see its stock and shelf, and I take a part so the stock drops and the part is linked to the repair.

## What it includes

- Search parts by name or part number, or browse the list; see stock and shelf; parts at or below their minimum are marked.
- "Take part" lowers the stock and links the part to the kart and the open repair, in one database transaction.
- Stock never goes below zero (`INVENTORY_STOCK_NEGATIVE`), and each request has its own id, so a double tap or a retry is not counted twice.
- Admins add, edit and archive parts, correct counts (logged) and set minimum levels.
- No QR or barcode scanning: parts are found by search or from a list.

## Planning

- **Sprint:** Sprint 3 (Must have).
- **December prototype:** In (part lookup and taking a part).
- **Requirements:** FR-42 to FR-44; US-17 to US-19 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[Data model](../03%20Architecture/Data%20model.md), [ADR-13 No QR codes](../10%20Decision%20Log/ADR-13%20No%20QR%20codes.md), [ADR-36 Engineering safeguards- jobs, stock moves, document revisions, test set, Supercube checklist](../10%20Decision%20Log/ADR-36%20Engineering%20safeguards-%20jobs,%20stock%20moves,%20document%20revisions,%20test%20set,%20Supercube%20checklist.md)
