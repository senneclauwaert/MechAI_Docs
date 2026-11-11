---
id: "ADR-5"
area: "AI"
status: "Superseded by ADR-27"
date: "2026-10-16"
tags: [decision]
updated: 2026-11-06
---
# ADR-5 Four-step retrieval: query rewrite, hybrid search, parent-document lookup, corrective relevance check

Back to [Decision Log](Decision%20Log.md)

**Status:** Superseded by ADR-27

**Context:** A comparison of known RAG techniques on 16 October 2026 proposed stacking four of them from the start.

**Decision:** Build query rewrite, hybrid search, parent-document lookup and a corrective relevance check in one go.

**Why:** Each technique fits a known problem of the handbook and the mechanics' questions.

**Alternatives considered:** Naive RAG, HyDE, agentic RAG.

**Consequences:** Replaced on 6 November 2026 by a baseline-first approach that adds steps one at a time. See [ADR-27 Baseline-first retrieval with English query translation](ADR-27%20Baseline-first%20retrieval%20with%20English%20query%20translation.md).
