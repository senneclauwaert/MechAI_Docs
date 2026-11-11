---
tags: [rag, index]
updated: 2026-11-06
---
# RAG and AI

Back to [Final Work Hub](../Final%20Work%20Hub.md)

This folder explains the repair assistant: *why* each choice was made, which options were compared and which earlier choices were replaced. The short version for the analysis is in [Technical Analysis (RAG, LLM & stack)](../02%20Analysis/Technical%20Analysis%20%28RAG,%20LLM%20&%20stack%29.md); the exact build steps are in [RAG pipeline (build spec)](../03%20Architecture/RAG%20pipeline%20%28build%20spec%29.md).

## How RAG works here, in five steps

1. The handbook is cut into small pieces called **chunks**.
2. Each chunk becomes an **embedding**: a list of numbers that represents its meaning, so texts with a similar meaning get similar numbers.
3. A mechanic's question gets an embedding too. The database finds the closest chunks (**vector search**) and at the same time runs a word search for exact part numbers and codes. Together that is **hybrid search**.
4. The best sections go to the **LLM** (large language model, the model that writes text) with one instruction: answer only from these sources and cite them.
5. Code checks the answer before the mechanic sees it.

## Notes in this folder

**Choosing the parts**

- [Answer model (LLM)](Answer%20model%20%28LLM%29.md): the OpenAI API, and how the choice evolved.
- [Embeddings and reranker](Embeddings%20and%20reranker.md): `text-embedding-3-small`, incremental updates and when a reranker is worth it.
- [Handbook ingestion and parsing](Handbook%20ingestion%20and%20parsing.md): the digital PDF, Docling, page images and wiring diagrams.
- [Vector storage and hybrid search](Vector%20storage%20and%20hybrid%20search.md): PostgreSQL with pgvector, full-text search and RRF.
- [Retrieval technique choice](Retrieval%20technique%20choice.md): the baseline first, and which known techniques we add or reject.
- [Framework choice](Framework%20choice.md): plain Python now; LangChain and LangGraph kept as options.

**Making the assistant good and safe**

- [Safety rules](Safety%20rules.md): the three safety levels enforced in code.
- [Evaluation](Evaluation.md): the test set, the metrics and the KPIs.
- [Optimization playbook](Optimization%20playbook.md): the ranked experiments, one change at a time.
- [Repair notes as knowledge](Repair%20notes%20as%20knowledge.md): how approved notes become a source.

**Related elsewhere**

- [Voice input and hands-free use](../05%20Features/Voice%20input%20and%20hands-free%20use.md) in Features.
- [Repair videos](../08%20Parked%20and%20Future%20Ideas/Repair%20videos.md) in Parked and Future Ideas.
