---
tags: [rag, knowledge]
updated: 2026-11-06
---
# Repair notes as knowledge

Back to [RAG and AI](RAG%20and%20AI.md) · Decision: [ADR-10 Repair notes become a source only after senior approval](../10%20Decision%20Log/ADR-10%20Repair%20notes%20become%20a%20source%20only%20after%20senior%20approval.md)

The handbook will never contain Supercube's own experience: what a mechanic learned while fixing a kart is not written down anywhere. Repair notes capture that knowledge, so the next mechanic with the same fault does not start from zero.

## Rules

- A repair note counts as a source **only after a senior mechanic approves it**.
- Approved notes always **rank below the handbook** and are **never the source of a safety step**.
- **Editing an approved note removes its approval** until a senior approves the new version. When a note is edited or retired, its chunks are removed from the search index.

## How it works

- After a repair, the mechanic fills in a short form: kart, symptom, cause, fix, parts used and optional photos. Kart and parts are picked from lists; the text can be spoken.
- A note moves through draft, in review, approved or rejected. A rejection goes back to the mechanic with a comment.
- A senior re-enters the PIN to approve, so every approval is tied to the right person.
- Approved notes are indexed with the source type "repair note" (only their own chunks are embedded).
- The assistant shows them in a separate "Similar past repairs" block, at most two per answer.
- The approval step also protects against prompt injection through notes ([Safety rules](Safety%20rules.md)).

## When

Semester 2. The December prototype focuses on the handbook, kart status, issues, stock and repairs. Notes are a natural next step because the repair log already exists by then.

See also the feature note [Repair notes with senior approval](../05%20Features/Repair%20notes%20with%20senior%20approval.md).
