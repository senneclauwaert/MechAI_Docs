---
tags: [rag, retrieval]
updated: 2026-11-06
---
# Retrieval technique choice

Back to [RAG and AI](RAG%20and%20AI.md) · Decisions: [ADR-27 Baseline-first retrieval with English query translation](../10%20Decision%20Log/ADR-27%20Baseline-first%20retrieval%20with%20English%20query%20translation.md), [ADR-22 Relevance check also ranks, cross-references are followed, one retry before refusing](../10%20Decision%20Log/ADR-22%20Relevance%20check%20also%20ranks,%20cross-references%20are%20followed,%20one%20retry%20before%20refusing.md)

**Retrieval** is the step that finds the handbook passages a question needs. Many techniques exist; this note says which ones MechAi uses, in which order, and which ones it rejects.

## Decision (6 November 2026): baseline first

Build the simplest reliable pipeline, measure it, then add one improvement at a time and keep it only if the test set improves.

**Baseline (December prototype):**

1. **Translate** the question into English search terms (the handbook is English; mechanics ask in Dutch, French or English).
2. **Hybrid search:** meaning search and exact word search, merged with RRF.
3. **Parent section:** search on small chunks, but send the whole section with its pages to the model.
4. **Cited answer:** every step cites its page; code checks numbers and citations.
5. **Refusal:** below the score threshold, "Not in the handbook, ask a senior mechanic", with the closest pages.

**Added one at a time, each kept only if it helps:**

6. **Relevance check with ranking:** one call scores every candidate section from 0 to 3, drops the zeros and re-orders the rest.
7. **Cross-references:** when a chosen section says "see section 5.3" or "table 4-2", add up to 2 of those sections.
8. **One retry:** if nothing passes, search once more with broader terms before refusing.
9. **Full query rewrite** if short or vague questions still fail.

## Every technique, rated for us

The comparison was first made on 16 October 2026 against the 13 techniques in the athina-ai "rag-cookbooks" collection, and checked again on 2 November against a popular RAG checklist.

| Technique | What it does, plainly | Verdict | Why |
| --- | --- | --- | --- |
| Naive RAG | Meaning search, paste the results into the prompt | Measured as the starting point | The "before" number for the evaluation |
| **Hybrid RAG** | Meaning search plus keyword search, merged | **Baseline** | Part numbers, torque values and failure codes need exact matching |
| **Query translation** | Turn the question into English search terms | **Baseline** | The handbook is English; Dutch keywords find nothing |
| **Parent document retrieval** | Search small chunks, send the whole section | **Baseline** | A procedure must reach the model whole, with no missing step |
| **Corrective RAG (without web search)** | Grade the found sections, drop bad ones | **Added if it helps** (step 6) | The grading step matches our "not in the handbook" rule; web search is never allowed |
| Rewrite-Retrieve-Read | The model rewrites the question before searching | **Added if it helps** (step 9) | Helps with short, vague questions; translation already covers the language part |
| Contextual chunk headers | Put "handbook > section > pages" in front of each chunk | **Baseline** | Cheap; expected to reduce failed searches (measured in experiment 4) |
| HyDE | The model writes a fake answer first and searches with it | Rejected | The fake answer can invent technical details that steer the search |
| Contextual compression | Cut retrieved text down to the "relevant" sentences | Rejected | It can cut a safety warning out of a procedure |
| RAG Fusion | Several versions of the question, searched and merged | Maybe later | Overlaps with translation and hybrid search, 3 to 5 times more searches |
| Self-RAG | The model checks its own answer | Maybe later | Our code already checks numbers and citations |
| Adaptive RAG | Route questions to different paths | Semester 2 idea | Could send stock and history questions to SQL instead of the handbook |
| GraphRAG | Build a knowledge graph of the documents | Rejected for now | Heavy to build and explain for one 89-page handbook |
| Agentic RAG, ReAct | An agent decides which tools to call, in a loop | Rejected | Unpredictable, slow and hard to test; not acceptable for safety answers |

## Why baseline first

- Two outside reviews (24 and 27 October) advised it: every extra step costs time and money, and may not help.
- Measuring each step separately gives clear before-and-after numbers for the jury.
- A smaller pipeline is easier to explain and to debug.

The order of the experiments is in the [Optimization playbook](Optimization%20playbook.md).
