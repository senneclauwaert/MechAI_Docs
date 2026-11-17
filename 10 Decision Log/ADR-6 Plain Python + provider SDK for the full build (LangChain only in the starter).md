---
id: "ADR-6"
area: "AI"
status: "Accepted"
date: "2026-10-16"
tags: [decision]
updated: 2026-11-17
---
# ADR-6 Plain Python + provider SDK for the full build

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · confirmed 6 Nov 2026

**Context:** A minimal LangChain starter existed. For the full build, the team must be able to explain every step of the pipeline.

**Decision:** The RAG code is plain Python with the AI provider's official SDK behind our own `LLMClient` (since 17 November 2026 the Mistral SDK, `mistralai`; see [ADR-38 Mistral API for answers, embeddings and speech-to-text](ADR-38%20Mistral%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md)). At most `langchain-text-splitters` is used. LangChain and LangGraph stay open as options if the pipeline grows. Confirmed on 6 November 2026.

**Why:** A handful of steps, each a function you can point at; easier debugging; no lock-in.

**Alternatives considered:** LangChain or LlamaIndex for the whole pipeline; LangGraph.

**Consequences:** The old LangChain starter is archived and no longer updated. See [Framework choice](../04%20RAG%20and%20AI/Framework%20choice.md).
