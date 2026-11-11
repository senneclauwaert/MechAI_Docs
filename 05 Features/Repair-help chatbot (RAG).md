---
id: "FEAT-5"
priority: "Must have"
area: "Assistant"
sprint: "Sprints 1 to 3"
december: "In"
tags: [feature]
updated: 2026-11-06
---
# Repair-help chatbot (RAG)

Back to [Features](Features.md)

## User story

As a mechanic, I pick a kart and ask my question out loud, and I get numbered steps with the handbook page for every step and the page shown as an image, or an honest "not in the handbook". Dangerous situations are handled by fixed rules, not by the AI.

## What it includes

- The mechanic picks a kart (or comes from the kart's page); it stays visible at the top.
- Questions by voice or text in Dutch, French or English; the answer comes back in the same language, quotes stay in English.
- Numbered steps, each citing its section and page; the cited pages are shown as images, tap to zoom. Electrical questions also show the wiring-diagram page.
- Three safety levels in code: emergency (STOP card, no AI), high voltage (Supercube's fixed text and the original pages, one logged confirmation), normal (cited steps). See [Safety rules](../04%20RAG%20and%20AI/Safety%20rules.md).
- Every number is checked against the cited page in code.
- Below the threshold: "Not in the handbook, ask a senior mechanic", with the closest pages.
- Retrieval-only mode when the AI is down or switched off.
- Step-by-step mode with read-aloud in semester 2.

## Planning

- **Sprint:** Sprints 1 to 3 (Must have).
- **December prototype:** In.
- **Requirements:** FR-01 to FR-15; US-04 to US-11 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[RAG pipeline (build spec)](../03%20Architecture/RAG%20pipeline%20%28build%20spec%29.md), [Retrieval technique choice](../04%20RAG%20and%20AI/Retrieval%20technique%20choice.md), [Answer model (LLM)](../04%20RAG%20and%20AI/Answer%20model%20%28LLM%29.md), [Voice input and hands-free use](Voice%20input%20and%20hands-free%20use.md), [Answer feedback and traces](Answer%20feedback%20and%20traces.md)
