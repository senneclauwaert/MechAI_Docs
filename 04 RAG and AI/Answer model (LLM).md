---
tags: [rag, llm]
updated: 2026-11-17
---
# Answer model (LLM)

Back to [RAG and AI](RAG%20and%20AI.md) · Decision: [ADR-38 Mistral API for answers, embeddings and speech-to-text](../10%20Decision%20Log/ADR-38%20Mistral%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md)

An LLM (large language model) is the part of the assistant that writes the answer. In RAG it does not need to know anything about karts itself: it only turns the passages that search found into clear, cited steps. That is why a small and cheap model is enough.

## Current decision (17 November 2026)

**The Mistral API**, for three jobs:

| Job | Model | Setting |
| --- | --- | --- |
| Writing answers and translating questions | Mistral Small (Mistral Small 4 at the time of writing) | `CHAT_MODEL` |
| Embeddings | `mistral-embed` (1,024 numbers per text) | `EMBED_MODEL` |
| Speech-to-text for voice questions | Voxtral Mini Transcribe | `STT_MODEL` |

**Why:**

- One provider covers all three jobs. Mistral is a French company with servers in the EU, which helps with Supercube's written OK.
- It is cheap: about $0.0015 per question and $5 to $8 a month for 3,000 questions ([Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md)).
- Small models follow instructions well, write structured JSON and handle Dutch, French and English.
- Before go-live we check Mistral's API terms on whether data can be used for training and switch that off where possible. Supercube's written OK is needed too ([Questions for Supercube](../01%20Project/Questions%20for%20Supercube.md)).

**Other models later.** Larger Mistral models and DeepSeek are tested later on the test set. If Supercube has its own AI account or contract, MechAi can switch to it. Only the configuration of `LLMClient` changes.

## Keep the model swappable

The model names live only in config, and the code calls the provider through one small class, `LLMClient`, with three methods: `chat(messages)`, `embed(texts)` and `transcribe(audio)`. Models get renamed or retired; when that happens, the evaluation script re-checks the replacement before it goes live.

## Cost guards

A monthly budget limit on the Mistral account, a question limit per user, a daily cap, a cap on answer length and an admin switch that turns AI answers off. Costs are estimated in [Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md).

## Images

The AI does **not** describe wiring diagrams or write wiring facts. Diagram pages are shown to the mechanic as images ([Handbook ingestion and parsing](Handbook%20ingestion%20and%20parsing.md)). Photo questions ("what is this part?") are a semester 2 idea and would use a vision-capable Mistral model.

## How the decision changed

| Date | Choice | What happened |
| --- | --- | --- |
| 5 Oct 2026 | Research advice: a local model through Ollama for development, a small Azure OpenAI model for the demo | Replaced on 6 October: local models need a strong GPU that is always on |
| 6 Oct 2026 | Claude Haiku 4.5 through the Anthropic API | Replaced on 10 October to keep one provider in Azure |
| 10 Oct 2026 | Azure OpenAI for answers and embeddings | Replaced on 6 November when Azure hosting was dropped |
| 6 Nov 2026 | OpenAI API directly, for answers, embeddings and speech-to-text | Replaced on 17 November: the team chose not to use OpenAI |
| 17 Nov 2026 | **Mistral API**, for answers, embeddings and speech-to-text | **Current decision** |
