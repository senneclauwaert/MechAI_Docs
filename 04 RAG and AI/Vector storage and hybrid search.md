---
tags: [rag, retrieval, database]
updated: 2026-11-06
---
# Vector storage and hybrid search

Back to [RAG and AI](RAG%20and%20AI.md) · Decision: [ADR-4 PostgreSQL + pgvector with hybrid search (RRF)](../10%20Decision%20Log/ADR-4%20PostgreSQL%20+%20pgvector%20with%20hybrid%20search%20%28RRF%29.md)

A **vector database** stores embeddings and finds the ones closest to the embedding of a question. An **index** is a shortcut structure that makes that search fast.

## Decision

**PostgreSQL with the pgvector extension**, an HNSW index, plus PostgreSQL full-text search, with both result lists merged by RRF.

**Why pgvector:**

- One database we already know (SQL), which also holds karts, stock and tasks: one backup, one container.
- Filters run in the same query as the search.
- Free and open source; the `pgvector/pgvector:pg16` Docker image includes it.
- Our scale is tiny: one handbook of 89 pages.

## One database, not two

A separate database for the assistant was considered. The choice is one database with a separate schema per module:

- The assistant's tables (`knowledge`, `assistant`) are already separated from the app's tables by their schema.
- Two databases would mean two containers to run, two backups and no way to link an answer to a kart in one query.
- If the assistant ever needs its own database, the schema can be moved without changing other modules.

## How hybrid search works

A **keyword search** and a **vector search** run at the same time and the results are merged.

- Keyword search finds exact codes and part numbers.
- Vector search finds meaning: "motor cuts out" matches "loss of drive".
- **RRF** (reciprocal rank fusion) merges the two ranked lists. Each result gets 1 / (60 + its rank) from each list, and the scores are added. It needs no tuning.

## Settings

- An **HNSW** index with cosine distance and the default settings.
- One `tsvector` column with the `english` configuration (the handbook is English) and a GIN index. Exact part numbers and failure codes are also matched with the `simple` configuration (no stemming).
- Keyword search cannot match across languages, so the question is first translated into English keywords ([ADR-27 Baseline-first retrieval with English query translation](../10%20Decision%20Log/ADR-27%20Baseline-first%20retrieval%20with%20English%20query%20translation.md)).
- Only the current document revision is searched.
- Every Supercube kart is the same model today; a `kart_model` column stays so a second model could be added later.

## Alternatives compared

| Option | Pros | Cons | Verdict |
| --- | --- | --- | --- |
| Chroma | Very easy for a quick test | A second database next to PostgreSQL | Only in the old starter |
| Qdrant, Pinecone, Weaviate | Fast, purpose-built | An extra service; Pinecone is cloud only | Only worth it at millions of chunks |
| Elasticsearch or OpenSearch | Strong keyword search | Heavy to run for one handbook | Not needed |
