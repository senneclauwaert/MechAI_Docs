---
id: "ADR-38"
area: "AI"
status: "Accepted"
date: "2026-11-17"
tags: [decision]
updated: 2026-11-17
---
# ADR-38 Mistral API for answers, embeddings and speech-to-text

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · replaces [ADR-25 OpenAI API for answers, embeddings and speech-to-text](ADR-25%20OpenAI%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md)

**Context:** ADR-25 chose the OpenAI API "for now". On 17 November 2026 the team decided not to use OpenAI and compared Mistral and DeepSeek.

**Decision:** The Mistral API for all three AI jobs, behind the same `LLMClient`:

- Search terms and answers: a small Mistral chat model (`CHAT_MODEL`, Mistral Small 4 at the time of writing).
- Embeddings: `mistral-embed` (`EMBED_MODEL`), 1,024 numbers per text.
- Speech-to-text for voice questions: Voxtral Mini Transcribe (`STT_MODEL`).

Other models, such as Mistral Large or DeepSeek, are tested later on the test set. Only the configuration changes.

**Why:**

- One provider covers chat, embeddings and speech-to-text: one key, one bill, one set of terms.
- Mistral is a French company with servers in the EU. That makes Supercube's written OK to send the handbook text easier.
- Low cost (Mistral price list, 17 November 2026): about $0.15 per million input tokens and $0.60 per million output tokens for Mistral Small, $0.10 per million tokens for embeddings and $0.0035 per minute of audio. That is roughly $5 to $8 a month for 3,000 questions.
- Mistral also publishes open-weight models, so Supercube could run a model on its own hardware later.

**Alternatives considered:**

- The OpenAI API ([ADR-25 OpenAI API for answers, embeddings and speech-to-text](ADR-25%20OpenAI%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md)): dropped by the team on 17 November 2026.
- DeepSeek: strong and cheap for chat, but its API offers no embeddings or speech-to-text, and its hosted API stores data in China. Kept as a model to test later.
- Local models: need a strong GPU that is always on (dropped on 6 October 2026).

**Consequences:**

- The embedding column becomes `vector(1024)`. The handbook is embedded with `mistral-embed` (a few minutes, under a cent) and the evaluation runs again.
- `MISTRAL_API_KEY` replaces the OpenAI key, and the server needs outgoing access to `api.mistral.ai`.
- Before go-live we check in Mistral's API terms whether data can be used for training, and switch that off if needed. Supercube's written OK is still required.
- A Mistral account with a monthly budget limit is needed (T-07).

See [Answer model (LLM)](../04%20RAG%20and%20AI/Answer%20model%20%28LLM%29.md) and [Embeddings and reranker](../04%20RAG%20and%20AI/Embeddings%20and%20reranker.md).
