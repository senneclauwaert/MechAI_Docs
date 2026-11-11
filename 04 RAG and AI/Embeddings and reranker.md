---
tags: [rag, retrieval]
updated: 2026-11-06
---
# Embeddings and reranker

Back to [RAG and AI](RAG%20and%20AI.md)

An **embedding model** turns a text into a list of numbers (a *vector*) so that texts with a similar meaning get similar numbers, even with different words: "remblokken" and "brake pads" end up close together. A **reranker** re-reads the top search results together with the question and puts the best one first.

## Current decision

**OpenAI `text-embedding-3-small`** through the OpenAI API ([ADR-25 OpenAI API for answers, embeddings and speech-to-text](../10%20Decision%20Log/ADR-25%20OpenAI%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md)). It produces 1,536 numbers per text, works across languages and is very cheap: about $0.02 per million tokens, so the whole handbook costs a fraction of a cent.

- Its Dutch and French quality is checked on our own test set.
- **Fallback:** `text-embedding-3-large`. Better but more expensive, with 3,072 numbers. The pgvector HNSW index accepts at most 2,000 dimensions, so the vectors would be shortened or stored as `halfvec`.

## New information does not mean re-embedding everything

A new manual page, part or kart does not mean rebuilding all embeddings:

- **New or changed text:** each chunk stores a `content_hash` (a fingerprint of its text). At ingestion, a chunk whose hash already exists keeps its embedding. Only new or changed chunks are sent to the embedding model. A new handbook revision with a few changed pages costs a few embeddings.
- **A new document** (for example a Supercube procedure) is simply added: only its own chunks are embedded.
- **New karts, parts or stock** are normal database rows. They are never embedded and have no effect on the search index.
- **Changing the embedding model** is the only case where everything is embedded again. For one handbook this takes a few minutes and costs less than a cent. The new vectors are built next to the old ones and switched on only after the evaluation passes.

## Earlier options

- **BGE-M3** (open source, run on our own machine) was the choice from 6 to 10 October 2026. It was strong on Dutch retrieval but needs our own hardware. It can still be used as a comparison in the evaluation.
- Other candidates from the research: multilingual-e5-large-instruct, Qwen3-Embedding. Our own test set decides if we ever run an embedding experiment.

## Reranker

A reranker is added only when the [Evaluation](Evaluation.md) shows that the right page is in the top 20 but not near the top (high recall@20, low recall@3). If recall@20 itself is low, a reranker cannot help; then we fix the chunking, the search terms or a missing document.

**First option (ADR-22):** let the relevance check score each section from 0 to 3 and sort by that score. This is a reranker built with the language model, without a separate model ([ADR-22 Relevance check also ranks, cross-references are followed, one retry before refusing](../10%20Decision%20Log/ADR-22%20Relevance%20check%20also%20ranks,%20cross-references%20are%20followed,%20one%20retry%20before%20refusing.md)).

**Second option, only if needed:** a dedicated open-source reranker model such as Qwen3-Reranker-0.6B or bge-reranker-v2-m3. jina-reranker-v2 is avoided because its licence forbids commercial use.
