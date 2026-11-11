---
id: "ADR-22"
area: "AI"
status: "Accepted"
date: "2026-11-02"
tags: [decision]
updated: 2026-11-06
---
# ADR-22 Relevance check also ranks, cross-references are followed, one retry before refusing

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted on 6 Nov 2026

**Context:** A widely shared RAG checklist was compared with our plan on 2 November 2026.

**Decision:** Three improvements, added after the baseline and each kept only if the test set improves: (1) the relevance check scores each section from 0 to 3 and re-orders them; (2) up to 2 sections referred to by a chosen section ("see section 5.3") are added; (3) if nothing passes, one broader search is tried before refusing. Accepted on 6 November 2026.

**Why:** Each addresses a real weakness for a handbook full of cross-references, at little cost.

**Alternatives considered:** A dedicated reranker model first; GraphRAG.

**Consequences:** Experiments 9 to 11 in the [Optimization playbook](../04%20RAG%20and%20AI/Optimization%20playbook.md).
