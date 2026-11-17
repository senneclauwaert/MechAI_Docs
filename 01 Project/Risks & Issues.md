---
tags: [project, risks]
updated: 2026-11-17
---
# Risks & Issues

Back to [Final Work Hub](../Final%20Work%20Hub.md)

This note lists what can go wrong and what we do about it. Impact and likelihood are rated High, Medium or Low. The biggest risks are the safety of high-voltage answers, the permissions we need from Supercube, and the time available for two people.

## Risk register

| Risk | Impact | Likelihood | Mitigation |
| --- | --- | --- | --- |
| **A wrong step on a high-voltage system** (a hallucination: a confident answer the sources don't support) | High | Medium | The AI never writes high-voltage or emergency steps: fixed Supercube texts and the original pages are shown instead. Every number is checked against the cited page. "Not in the handbook" when the sources are weak. A senior safety review before the Showdown. See [Safety rules](../04%20RAG%20and%20AI/Safety%20rules.md) |
| **No written permission** to use the handbook with an AI service | High | Medium | Ask Supercube now with one signed checklist ([Questions for Supercube](Questions%20for%20Supercube.md)). Until then, develop with a few test pages only |
| **No access to Supercube's API or test environment** | Medium | Medium | The `supercube` module has a fake client with demo data, so the prototype does not depend on it |
| **Diagnostics started from MechAi while someone works on the kart** | High | Medium | A "nobody at the kart" confirmation before the first mode; an automatic stop after 60 seconds without a command; diagnostics blocked while someone else has an open repair on that kart; every start and stop logged with the person; a big Stop button. The real connection only after Supercube's written OK |
| **No server or HTTPS certificate on the internal network** | High | Medium | A PWA, the camera and the microphone need HTTPS. Ask Supercube IT early for a server, an internal hostname and a certificate. Develop locally with Docker Compose in the meantime |
| **Scope creep** (3D, notifications, videos and so on) | High | High | Scope freeze until the December demo; parked ideas in [Parked and future ideas](../08%20Parked%20and%20Future%20Ideas/Parked%20and%20future%20ideas.md) |
| **Code gets too complex to explain** | Medium | Medium | One module template for every feature, automatic formatting and linting, review by the other person |
| **The question's language differs from the handbook's** (Dutch or French question, English handbook) | Medium | High | The question is translated into English search terms in the baseline; cross-language test questions |
| **AI costs higher than expected** | Low | Low | A monthly budget limit on the Mistral account, a question limit per user, a daily cap and a switch that turns AI answers off |
| **Mistral or the internet connection is down during the demo** | High | Low | Retrieval-only mode (show the pages without generated steps) and a recorded backup video |
| **Prompt injection through repair notes** (text that tries to give the model new orders) | Medium | Low | Notes count only after senior approval, sources are passed as data, planted-attack tests |
| **Privacy:** handbook text sent to the AI provider (Mistral), or kept in logs | High | Medium | Supercube's written OK first; the full text is sent once per version for the search index and only the matching sections per question; until the OK, only a few test pages are used; traces stay in our own database on Supercube's server |
| **Photos show people or private details** | Medium | Low | A rule not to photograph people; photos stay on Supercube's server and are only served after login |
| **Data loss on the server** | High | Low | Nightly backup of the database and the file volume, agreed with Supercube IT |
| **Model retired or renamed** | Low | Medium | Model names only in config, one `LLMClient`, and the evaluation script to re-check a replacement |
| **Team member unavailable** | Medium | Low | Pull-request reviews by both, a README that gets anyone running quickly, everything in git |

## Resolved risks

- **Microservice complexity for two people.** Solved by the modular monolith ([ADR-1 Modular monolith- one backend + one worker + one PostgreSQL, no microservices](../10%20Decision%20Log/ADR-1%20Modular%20monolith-%20one%20backend%20+%20one%20worker%20+%20one%20PostgreSQL,%20no%20microservices.md)).
- **No PDF of the handbook / poor photos.** Solved on 6 November 2026: the handbook is a digital PDF with real text.
- **Azure student subscription without AI quota, and cloud credit running out.** No longer relevant since 6 November 2026: MechAi runs on Supercube's servers and uses an AI API directly (Mistral since 17 November 2026) ([ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](../10%20Decision%20Log/ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md), [ADR-25 OpenAI API for answers, embeddings and speech-to-text](../10%20Decision%20Log/ADR-25%20OpenAI%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md)).
- **The app reachable by anyone who knows the URL.** Solved: MechAi is only reachable on Supercube's internal network.
