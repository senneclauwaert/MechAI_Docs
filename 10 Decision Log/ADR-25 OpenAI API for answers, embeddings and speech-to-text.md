---
id: "ADR-25"
area: "AI"
status: "Superseded by ADR-38"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-17
---
# ADR-25 OpenAI API for answers, embeddings and speech-to-text

Back to [Decision Log](Decision%20Log.md)

**Status:** Superseded by [ADR-38 Mistral API for answers, embeddings and speech-to-text](ADR-38%20Mistral%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md) on 17 November 2026

**Context:** With Azure hosting dropped, Azure OpenAI was no longer the obvious choice.

**Decision:** The OpenAI API directly: a small chat model for answers and translation, `text-embedding-3-small` for embeddings, and an OpenAI speech-to-text model for voice questions, behind one `LLMClient`. For now, until Supercube says whether it has its own AI account.

**Why:** One provider for all three jobs; no local GPU needed; very low cost; the provider can change in one place.

**Alternatives considered:** Azure OpenAI; Claude; local models.

**Consequences:** Needs Supercube's written OK to send the handbook text (the full text once per version for embeddings, the matching sections per question). A monthly budget limit and usage caps are required. See [Answer model (LLM)](../04%20RAG%20and%20AI/Answer%20model%20%28LLM%29.md).
