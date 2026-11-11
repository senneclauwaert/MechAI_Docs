---
tags: [reviews]
updated: 2026-11-06
---
# Reviews and proposals

Back to [Final Work Hub](../Final%20Work%20Hub.md)

Between 24 October and 2 November 2026 the plan was checked by two AI-assisted architecture reviews (one made with Antigravity, one with Claude) and against a widely shared checklist of RAG good practices. On 6 November 2026 Senne went through every proposal and decided on each one; Nehad still has to confirm them. This note summarises the outcome; every accepted change is recorded in the [Decision Log](../10%20Decision%20Log/Decision%20Log.md).

## What the reviews confirmed

Both reviews accepted the core design: the modular monolith (one backend, one worker, one PostgreSQL database with pgvector), hybrid search with RRF, Docling for parsing, one `LLMClient` for the AI provider, a job queue in PostgreSQL, the profile picker with a personal PIN, and approved repair notes ranked below the handbook. Their proposals were about safety, scope and order, not about the architecture.

## Outcome of each proposal

| Proposal | Outcome | Recorded in |
| --- | --- | --- |
| Safety levels: emergencies get a fixed STOP card with no AI; high-voltage work shows fixed text and the original pages; the stricter level wins | **Accepted** | [ADR-30 Safety levels enforced in code](../10%20Decision%20Log/ADR-30%20Safety%20levels%20enforced%20in%20code.md) |
| A device setup code per tablet in front of the PIN screen | **Not needed:** MechAi is only reachable on Supercube's internal network | [ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](../10%20Decision%20Log/ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md) |
| A trimmed December scope: one complete, measured workflow | **Accepted**, built for every kart | [ADR-35 Prototype scope- one complete workshop flow for all karts at one venue](../10%20Decision%20Log/ADR-35%20Prototype%20scope-%20one%20complete%20workshop%20flow%20for%20all%20karts%20at%20one%20venue.md) |
| Run the December demo locally; create cloud resources only later | **Replaced:** no cloud at all; MechAi runs on Supercube's server | [ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](../10%20Decision%20Log/ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md) |
| Simplest retrieval first; add the rewrite and the relevance check only when the tests improve | **Accepted**, with English query translation in the baseline | [ADR-27 Baseline-first retrieval with English query translation](../10%20Decision%20Log/ADR-27%20Baseline-first%20retrieval%20with%20English%20query%20translation.md) |
| Run ingestion on a laptop | **Not needed:** the PDF is digital (no OCR), so ingestion runs in the worker on the server | [ADR-17 Docling for parsing and OCR](../10%20Decision%20Log/ADR-17%20Docling%20for%20parsing%20and%20OCR.md) |
| Translate keywords into the handbook's language | **Accepted** (English) | [ADR-27 Baseline-first retrieval with English query translation](../10%20Decision%20Log/ADR-27%20Baseline-first%20retrieval%20with%20English%20query%20translation.md) |
| Move the 3D view to semester 2 | **Accepted** | [ADR-35 Prototype scope- one complete workshop flow for all karts at one venue](../10%20Decision%20Log/ADR-35%20Prototype%20scope-%20one%20complete%20workshop%20flow%20for%20all%20karts%20at%20one%20venue.md) |
| No AI-written wiring facts; show the diagram page | **Accepted** | [ADR-29 Citations come from the digital handbook PDF; pages shown as images](../10%20Decision%20Log/ADR-29%20Citations%20come%20from%20the%20digital%20handbook%20PDF;%20pages%20shown%20as%20images.md) |
| Safer jobs, safe stock moves, document revisions, a richer test set, a signed permissions checklist | **Accepted** | [ADR-36 Engineering safeguards- jobs, stock moves, document revisions, test set, Supercube checklist](../10%20Decision%20Log/ADR-36%20Engineering%20safeguards-%20jobs,%20stock%20moves,%20document%20revisions,%20test%20set,%20Supercube%20checklist.md) |
| Editing an approved repair note removes its approval | **Accepted** | [ADR-10 Repair notes become a source only after senior approval](../10%20Decision%20Log/ADR-10%20Repair%20notes%20become%20a%20source%20only%20after%20senior%20approval.md) |
| An EU data-zone deployment of the AI model | **No longer relevant:** the AI provider is the OpenAI API, with Supercube's written OK | [ADR-25 OpenAI API for answers, embeddings and speech-to-text](../10%20Decision%20Log/ADR-25%20OpenAI%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md) |
| Relevance check ranks (0 to 3), cross-references are followed, one retry before refusing | **Accepted**, each kept only if the tests improve | [ADR-22 Relevance check also ranks, cross-references are followed, one retry before refusing](../10%20Decision%20Log/ADR-22%20Relevance%20check%20also%20ranks,%20cross-references%20are%20followed,%20one%20retry%20before%20refusing.md) |
| GraphRAG, HyDE and contextual compression | **Rejected** for one 89-page handbook | [Retrieval technique choice](../04%20RAG%20and%20AI/Retrieval%20technique%20choice.md) |

## Decisions added by the team on 6 November 2026

Next to the review proposals, the team decided: self-hosting with Docker Compose, the OpenAI API, an operator role, diagnostics and kart status through Supercube's API, a hands-free design with voice input, one error format with error codes, strict code-quality rules, and sharing the documentation through a private GitHub repository. All are in the [Decision Log](../10%20Decision%20Log/Decision%20Log.md).

## AI-assisted review of the vault (6 November 2026, evening)

The whole vault was read once more by an AI reviewer. Its main points and what was done:

| Point | What changed |
| --- | --- |
| The full handbook text goes to OpenAI for embeddings, not only short excerpts | The permission question, pitch, risks and planning now say so. Only test pages are used until Supercube's written OK |
| Removing a failed step makes a procedure look complete | If any number check fails, no steps are shown, only the pages |
| Diagnostics move a kart while someone may be working on it | A "nobody at the kart" check, an automatic stop after 60 seconds, a block during an open repair; risk raised to Medium |
| The CI evaluation can't use the real handbook or skip AI calls | CI uses a small fake manual with cached embeddings; the real evaluation runs on the server per handbook version |
| The docs overstated how reviews and decisions were made | Reviews are named AI-assisted; decisions are marked as Senne's, to be confirmed by Nehad (T-43); an AI-use statement is planned (T-44) |
| The refusal threshold can't use RRF scores | The threshold uses cosine similarity or the relevance check |
| A failed "broken" call could leave an unsafe kart in play | Saved locally as "broken, not synced", retried, with a banner |
| Smaller contradictions, missing information and wording | Fixed in the notes; open items are in [Open questions](../01%20Project/Open%20questions.md) |
