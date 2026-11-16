---
tags: [hub]
updated: 2026-11-06
---
# Final Work Hub

> [!NOTE]
> **MechAi: a workshop assistant for the mechanics at Supercube.**
> MechAi is the Final Work of Senne Clauwaert and Nehad (Applied Informatics, Erasmushogeschool Brussel, 2026-2027). It is a web app for the kart mechanics at Supercube's Brussels venue. Its core is a repair assistant that answers questions from the kart manufacturer's handbook and always shows the page it used. Around it sit the kart status and service history, photo issues, parts stock, to-dos and notifications, and a link to Supercube's own kart system. MechAi runs on Supercube's own servers with Docker and is reachable only on Supercube's internal network.

This page is the entry point of the documentation. Every note can be reached from here in one or two clicks.

## How the documentation is organised

| Folder | Start note | What you find there |
| --- | --- | --- |
| 01 Project | [Project overview](01%20Project/Project%20overview.md) | What we build and why, the pitch, the team, the planning, the risks, open questions and the questions for Supercube |
| 02 Analysis | [Analysis](02%20Analysis/Analysis.md) | The analysis: problem, users, current and future situation, requirements, market, technical choices and user stories |
| 03 Architecture | [Architecture](03%20Architecture/Architecture.md) | How MechAi is built: modules, data model, API, the Supercube integration, the RAG pipeline, hosting, error handling and the repository setup |
| 04 RAG and AI | [RAG and AI](04%20RAG%20and%20AI/RAG%20and%20AI.md) | How the repair assistant works: model choice, handbook parsing, search, safety, evaluation and tuning |
| 05 Features | [Features](05%20Features/Features.md) | One note per feature, with its priority, planning and status |
| 06 Design and Prototypes | [Design and prototypes](06%20Design%20and%20Prototypes/Design%20and%20prototypes.md) | The official HTML prototype, the Figma design, the 3D kart view and the diagrams |
| 07 Reviews and Proposals | [Reviews and proposals](07%20Reviews%20and%20Proposals/Reviews%20and%20proposals.md) | The outside reviews of our plan and what we changed because of them |
| 08 Parked and Future Ideas | [Parked and future ideas](08%20Parked%20and%20Future%20Ideas/Parked%20and%20future%20ideas.md) | Ideas we chose not to build now, and options for later |
| 09 To Do | [To Do](09%20To%20Do/To%20Do.md) | The task list per sprint |
| 10 Decision Log | [Decision Log](10%20Decision%20Log/Decision%20Log.md) | Every important decision with its date, reason and alternatives |
| 11 Reference | [Glossary](11%20Reference/Glossary.md) | Glossary, sources and project links |

## Status on 6 November 2026

- **All design decisions are recorded.** On 6 November Senne reviewed every decision and open proposal one by one; Nehad still has to confirm them (T-43). The results are in the [Decision Log](10%20Decision%20Log/Decision%20Log.md) (ADR-1 to ADR-36).
- **The handbook is available.** Supercube provided the OTL "KART STORM User and Maintenance Handbook" as a digital PDF (89 pages, English). It contains real text, so no scanning or OCR is needed. See [Handbook ingestion and parsing](04%20RAG%20and%20AI/Handbook%20ingestion%20and%20parsing.md).
- **Supercube shared its GraphQL API schema.** MechAi will read kart status and alerts from it and can mark karts broken or repaired and run diagnostics. See [Supercube integration (GraphQL)](03%20Architecture/Supercube%20integration%20%28GraphQL%29.md).
- **Hosting is chosen; the server is still to confirm.** MechAi runs with Docker Compose on Supercube's own servers, only inside the internal network. Which server is **to confirm** with Supercube IT. Fallback for the December demo: Docker Compose on a team laptop. See [Hosting and deployment](03%20Architecture/Hosting%20and%20deployment.md).
- **Building starts on 9 November** with sprint 1. Nothing is built yet apart from the design prototype. See [Planning & Deadlines](01%20Project/Planning%20&%20Deadlines.md) and [To Do](09%20To%20Do/To%20Do.md).
- **Several answers from Supercube are needed** before parts of the system can be finished: API access, server details, permission to use the handbook with an AI service, and the fixed safety texts. See [Questions for Supercube](01%20Project/Questions%20for%20Supercube.md).

## How firm a statement is

The documentation uses the same words everywhere, so a reader always knows how firm a statement is.

- **Decided** (or **Accepted** in the Decision Log): agreed by the team. A change is logged as a new decision.
- **To confirm:** our current assumption, which still needs an answer from Supercube, the school or the team.
- **Superseded:** an earlier decision that a later one replaced. It is kept, with the reason, in [Superseded decisions](10%20Decision%20Log/Superseded%20decisions.md).

## Quick links

- **Official prototype:** [clickable HTML prototype](https://claude.ai/artifact/JoYu88yrzKTxP49N18dp3D)
- **Design:** [Figma "Prototype"](https://www.figma.com/design/hWB597CW9ZjhYQPv3eu5DG), with every v0.7 screen on the page ["v0.7 prototype (6 Nov 2026)"](https://www.figma.com/design/hWB597CW9ZjhYQPv3eu5DG?node-id=72-793)
- **Code:** the private GitHub repository for the code is created in sprint 1.
- All other links are in [Project links](11%20Reference/Project%20links.md).
