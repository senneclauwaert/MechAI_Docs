---
id: "ADR-30"
area: "Safety"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-30 Safety levels enforced in code

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** The karts have high-voltage batteries. Both outside reviews argued that a language model must not write safety plans.

**Decision:** Three levels. **Emergency:** a STOP card with Supercube's text, no AI. **High voltage:** Supercube's fixed text and the original pages, with one logged confirmation, no AI-written steps. **Normal:** cited steps with a number check. Code word lists and the AI's flag decide the level; the stricter level wins. Supercube writes the fixed texts.

**Why:** Safety does not depend on the AI being right.

**Alternatives considered:** AI-written steps unlocked after four checkboxes (the first prototype).

**Consequences:** See [Safety rules](../04%20RAG%20and%20AI/Safety%20rules.md).
