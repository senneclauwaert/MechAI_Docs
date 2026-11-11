---
id: "ADR-14"
area: "Architecture"
status: "Accepted"
date: "2026-10-24"
tags: [decision]
updated: 2026-11-06
---
# ADR-14 Photo issues: one Issue record linked to history, to-dos and alerts

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · amended 6 Nov 2026

**Context:** Visible problems on a kart (damage, loose cables, worn parts) get lost when passed on by word of mouth.

**Decision:** A reported problem is one Issue record (kart, reason, description, photos, severity, status). The kart history, to-dos and alerts point to that record. Since 6 November 2026 the operator can report issues too.

**Why:** No copies of the same data; one place to close the issue.

**Alternatives considered:** Separate photo lists per feature.

**Consequences:** Photos are stored through the `storage` module ([ADR-28 Files on a Docker volume behind one storage module](ADR-28%20Files%20on%20a%20Docker%20volume%20behind%20one%20storage%20module.md)).
