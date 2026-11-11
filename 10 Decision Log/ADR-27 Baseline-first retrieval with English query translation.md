---
id: "ADR-27"
area: "AI"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-27 Baseline-first retrieval with English query translation

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** The outside reviews advised building the simplest pipeline first. The handbook is in English; mechanics ask in Dutch, French or English.

**Decision:** The baseline translates the question into English search terms, runs hybrid search, takes the parent section, answers with citations and refuses below a threshold. Further steps (ADR-22 and a full rewrite) are added one at a time and kept only if the test set improves.

**Why:** Clear before-and-after numbers, less cost, easier to explain. Keyword search cannot match across languages, so translation belongs in the baseline.

**Alternatives considered:** All four steps at once (ADR-5); HyDE; GraphRAG.

**Consequences:** See [Retrieval technique choice](../04%20RAG%20and%20AI/Retrieval%20technique%20choice.md) and [Optimization playbook](../04%20RAG%20and%20AI/Optimization%20playbook.md).
