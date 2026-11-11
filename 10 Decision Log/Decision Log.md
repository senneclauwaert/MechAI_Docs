---
tags: [decision, index]
updated: 2026-11-06
---
# Decision Log

Back to [Final Work Hub](../Final%20Work%20Hub.md)

This log records every important choice. Each decision has its own note, an **ADR** (architecture decision record), with the context, the decision, the reason, the alternatives and the consequences. All decisions were reviewed with the team on 6 November 2026.

## Current decisions

| ID | Date | Decision | Area | Status |
| --- | --- | --- | --- | --- |
| ADR-36 | 2026-11-06 | [Engineering safeguards: jobs, stock moves, document revisions, test set, Supercube checklist](ADR-36%20Engineering%20safeguards-%20jobs,%20stock%20moves,%20document%20revisions,%20test%20set,%20Supercube%20checklist.md) | Architecture | Accepted |
| ADR-35 | 2026-11-06 | [Prototype scope: one complete workshop flow for all karts at one venue](ADR-35%20Prototype%20scope-%20one%20complete%20workshop%20flow%20for%20all%20karts%20at%20one%20venue.md) | Scope | Accepted |
| ADR-34 | 2026-11-06 | [The HTML prototype is the official design; diagrams as Mermaid in the vault](ADR-34%20The%20HTML%20prototype%20is%20the%20official%20design;%20diagrams%20as%20Mermaid%20in%20the%20vault.md) | Process | Accepted |
| ADR-33 | 2026-11-06 | [Docs shared through a private GitHub repository; internal notes kept apart](ADR-33%20Docs%20shared%20through%20a%20private%20GitHub%20repository;%20internal%20notes%20kept%20apart.md) | Process | Accepted |
| ADR-32 | 2026-11-06 | [One error format with module error codes](ADR-32%20One%20error%20format%20with%20module%20error%20codes.md) | Architecture | Accepted |
| ADR-31 | 2026-11-06 | [Hands-free design: voice input, quick picks, big buttons](ADR-31%20Hands-free%20design-%20voice%20input,%20quick%20picks,%20big%20buttons.md) | Frontend | Accepted |
| ADR-30 | 2026-11-06 | [Safety levels enforced in code](ADR-30%20Safety%20levels%20enforced%20in%20code.md) | Safety | Accepted |
| ADR-29 | 2026-11-06 | [Citations come from the digital handbook PDF; pages shown as images](ADR-29%20Citations%20come%20from%20the%20digital%20handbook%20PDF;%20pages%20shown%20as%20images.md) | AI | Accepted |
| ADR-28 | 2026-11-06 | [Files on a Docker volume behind one storage module](ADR-28%20Files%20on%20a%20Docker%20volume%20behind%20one%20storage%20module.md) | Architecture | Accepted |
| ADR-27 | 2026-11-06 | [Baseline-first retrieval with English query translation](ADR-27%20Baseline-first%20retrieval%20with%20English%20query%20translation.md) | AI | Accepted |
| ADR-26 | 2026-11-06 | [Four roles: operator, mechanic, senior mechanic, admin](ADR-26%20Four%20roles-%20operator,%20mechanic,%20senior%20mechanic,%20admin.md) | Security | Accepted |
| ADR-25 | 2026-11-06 | [OpenAI API for answers, embeddings and speech-to-text](ADR-25%20OpenAI%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md) | AI | Accepted |
| ADR-24 | 2026-11-06 | [Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md) | Hosting | Accepted |
| ADR-23 | 2026-11-06 | [Keep REST for our own API; talk to Supercube's GraphQL API through one adapter module](ADR-23%20Keep%20REST%20for%20our%20own%20API,%20talk%20to%20Supercube's%20GraphQL%20API%20through%20one%20adapter%20module.md) | Architecture | Accepted |
| ADR-22 | 2026-11-02 | [Relevance check also ranks, cross-references are followed, one retry before refusing](ADR-22%20Relevance%20check%20also%20ranks,%20cross-references%20are%20followed,%20one%20retry%20before%20refusing.md) | AI | Accepted |
| ADR-16 | 2026-10-24 | [Project docs moved from Notion to the Obsidian vault MechAi](ADR-16%20Project%20docs%20moved%20from%20Notion%20to%20the%20Obsidian%20vault%20MechAi.md) | Process | Accepted |
| ADR-15 | 2026-10-24 | [Simple, readable code with one copy-paste module template](ADR-15%20Simple,%20readable%20code%20with%20one%20copy-paste%20module%20template.md) | Process | Accepted |
| ADR-14 | 2026-10-24 | [Photo issues: one Issue record linked to history, to-dos and alerts](ADR-14%20Photo%20issues-%20one%20Issue%20record%20linked%20to%20history,%20to-dos%20and%20alerts.md) | Architecture | Accepted |
| ADR-13 | 2026-10-24 | [No QR codes](ADR-13%20No%20QR%20codes.md) | Frontend | Accepted |
| ADR-12 | 2026-10-16 | [No accounts: profile picker + personal PIN, 30-minute idle logout](ADR-12%20No%20accounts-%20profile%20picker%20+%20personal%20PIN,%2030-minute%20idle%20logout.md) | Security | Accepted |
| ADR-9 | 2026-10-16 | [Store answer traces in our own Postgres table](ADR-9%20Store%20answer%20traces%20in%20our%20own%20Postgres%20table.md) | AI | Accepted |
| ADR-8 | 2026-10-16 | [Frontend: React + TypeScript + Vite PWA, three.js for the 3D exploded view](ADR-8%20Frontend-%20React%20+%20TypeScript%20+%20Vite%20PWA,%20three.js%20for%20the%203D%20exploded%20view.md) | Frontend | Accepted |
| ADR-7 | 2026-10-16 | [Backend: Python 3.12, FastAPI, SQLAlchemy 2, Alembic](ADR-7%20Backend-%20Python%203.12,%20FastAPI,%20SQLAlchemy%202,%20Alembic.md) | Architecture | Accepted |
| ADR-6 | 2026-10-16 | [Plain Python + OpenAI SDK for the full build](ADR-6%20Plain%20Python%20+%20OpenAI%20SDK%20for%20the%20full%20build%20%28LangChain%20only%20in%20the%20starter%29.md) | AI | Accepted |
| ADR-11 | 2026-10-10 | [Repair videos parked](ADR-11%20Repair%20videos%20parked.md) | Scope | Accepted |
| ADR-10 | 2026-10-06 | [Repair notes become a source only after senior approval](ADR-10%20Repair%20notes%20become%20a%20source%20only%20after%20senior%20approval.md) | AI | Accepted |
| ADR-1 | 2026-10-06 | [Modular monolith: one backend + one worker + one PostgreSQL, no microservices](ADR-1%20Modular%20monolith-%20one%20backend%20+%20one%20worker%20+%20one%20PostgreSQL,%20no%20microservices.md) | Architecture | Accepted |
| ADR-18 | 2026-10-05 | [The frontend is a PWA](ADR-18%20The%20frontend%20is%20a%20PWA.md) | Frontend | Accepted |
| ADR-17 | 2026-10-05 | [Docling for parsing](ADR-17%20Docling%20for%20parsing%20and%20OCR.md) | AI | Accepted |
| ADR-4 | 2026-10-05 | [PostgreSQL + pgvector with hybrid search (RRF)](ADR-4%20PostgreSQL%20+%20pgvector%20with%20hybrid%20search%20%28RRF%29.md) | Database | Accepted |

## Replaced decisions

These ADRs were replaced by a later decision. They are kept so the analysis can explain how the plan evolved. Earlier ideas that never had an ADR are listed in [Superseded decisions](Superseded%20decisions.md).

| ID | Date | Decision | Replaced by |
| --- | --- | --- | --- |
| ADR-2 | 2026-10-10 | [Azure OpenAI for the answer model and embeddings](ADR-2%20Azure%20OpenAI%20for%20the%20answer%20model%20and%20embeddings.md) | ADR-25 |
| ADR-3 | 2026-10-10 | [Azure managed services, not a VM](ADR-3%20Azure%20managed%20services,%20not%20a%20VM.md) | ADR-24 |
| ADR-5 | 2026-10-16 | [Four-step retrieval: query rewrite, hybrid search, parent-document lookup, corrective relevance check](ADR-5%20Four-step%20retrieval-%20query%20rewrite,%20hybrid%20search,%20parent-document%20lookup,%20corrective%20relevance%20check.md) | ADR-27 |
| ADR-19 | 2026-10-06 | [Book photos are named by page number](ADR-19%20Book%20photos%20are%20named%20by%20page%20number,%20because%20the%20page%20is%20the%20citation.md) | ADR-29 |
| ADR-20 | 2026-10-06 | [Minimal LangChain starter accepted for the prototype](ADR-20%20Minimal%20LangChain%20starter%20accepted%20for%20the%20prototype.md) | ADR-6 |
| ADR-21 | 2026-10-06 | [UI design in Figma, diagrams in FigJam](ADR-21%20UI%20design%20in%20Figma,%20diagrams%20in%20FigJam.md) | ADR-34 |
