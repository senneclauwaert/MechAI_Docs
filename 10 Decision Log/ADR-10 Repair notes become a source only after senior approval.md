---
id: "ADR-10"
area: "AI"
status: "Accepted"
date: "2026-10-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-10 Repair notes become a source only after senior approval

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · amended 6 Nov 2026

**Context:** Mechanics' experience is valuable, but an unchecked note could be wrong or contain text that tries to steer the AI.

**Decision:** A repair note becomes searchable only after a senior mechanic approves it (re-entering the PIN). Approved notes rank below the handbook and are never the source of a safety step. Editing an approved note removes its approval (added 6 November 2026).

**Why:** Keeps the knowledge base correct and protects against prompt injection.

**Alternatives considered:** Every note searchable at once; no notes at all.

**Consequences:** Semester 2 feature. See [Repair notes as knowledge](../04%20RAG%20and%20AI/Repair%20notes%20as%20knowledge.md).
