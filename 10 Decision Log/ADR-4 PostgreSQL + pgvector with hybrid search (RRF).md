---
id: "ADR-4"
area: "Database"
status: "Accepted"
date: "2026-10-05"
tags: [decision]
updated: 2026-11-06
---
# ADR-4 PostgreSQL + pgvector with hybrid search (RRF)

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** The assistant needs a vector store, and the app needs a normal database for karts, stock and tasks.

**Decision:** One PostgreSQL database with the pgvector extension, an HNSW index and PostgreSQL full-text search, merged with reciprocal rank fusion (RRF). One schema per module. Reconfirmed on 6 November 2026, when a separate database for the assistant was considered.

**Why:** One database the team already knows, one backup and one container. Filters and joins work in the same query. Our scale is one 89-page handbook.

**Alternatives considered:** A second database only for the assistant; Chroma; Qdrant, Weaviate or Pinecone; Elasticsearch.

**Consequences:** The `pgvector/pgvector:pg16` image is used. See [Vector storage and hybrid search](../04%20RAG%20and%20AI/Vector%20storage%20and%20hybrid%20search.md).
