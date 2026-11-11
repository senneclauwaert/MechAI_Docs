---
id: "ADR-2"
area: "AI"
status: "Superseded by ADR-25"
date: "2026-10-10"
tags: [decision]
updated: 2026-11-06
---
# ADR-2 Azure OpenAI for the answer model and embeddings

Back to [Decision Log](Decision%20Log.md)

**Status:** Superseded by ADR-25

**Context:** The project was going to run on Azure with the student credit.

**Decision:** Azure OpenAI for both the answer model and the embeddings.

**Why:** One provider, one bill and one EU region with the rest of the Azure hosting.

**Alternatives considered:** Claude Haiku 4.5 (the choice of 6 October), local models.

**Consequences:** Replaced on 6 November 2026 when Azure hosting was dropped. See [ADR-25 OpenAI API for answers, embeddings and speech-to-text](ADR-25%20OpenAI%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md).
