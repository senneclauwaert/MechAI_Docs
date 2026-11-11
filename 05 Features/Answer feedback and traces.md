---
id: "FEAT-11"
priority: "Must have"
area: "Assistant"
sprint: "Sprint 3"
december: "In"
tags: [feature]
updated: 2026-11-06
---
# Answer feedback and traces

Back to [Features](Features.md)

## User story

As a mechanic, I give a thumbs down with a quick reason; as the team, we see exactly which pages, prompt and model produced that answer.

## What it includes

- Every answer has thumbs up and down; thumbs down asks for a reason with buttons (wrong kart, wrong page, wrong step, unsafe, missing step, other).
- Each rating is linked to a trace with the retrieved chunks, scores, prompt version, model, document revision, tokens, cost, latency and error code.
- Traces live in our own PostgreSQL table and feed the evaluation chapter.

## Planning

- **Sprint:** Sprint 3 (Must have).
- **December prototype:** In.
- **Requirements:** FR-10; US-10 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[ADR-9 Store answer traces in our own Postgres table](../10%20Decision%20Log/ADR-9%20Store%20answer%20traces%20in%20our%20own%20Postgres%20table.md), [Evaluation](../04%20RAG%20and%20AI/Evaluation.md)
