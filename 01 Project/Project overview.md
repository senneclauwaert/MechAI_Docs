---
tags: [project]
updated: 2026-11-06
---
# Project overview

Back to [Final Work Hub](../Final%20Work%20Hub.md)

This note explains the project on one page: what we build, for whom, under which constraints, and how it is graded. The other notes in this folder go deeper: [Pitch & WHY](Pitch%20&%20WHY.md), [Team & Agreements](Team%20&%20Agreements.md), [Planning & Deadlines](Planning%20&%20Deadlines.md), [Risks & Issues](Risks%20&%20Issues.md), [Open questions](Open%20questions.md) and [Questions for Supercube](Questions%20for%20Supercube.md).

## What we build

**Supercube** runs AR karting (augmented-reality karting): drivers wear a headset and race identical single-seat electric karts on a "gaming floor". Senne works there as a mechanic, so the project has a real user and a real problem. The project covers **one venue, Brussels**. The data model keeps a venue field, so other venues can be added later without changes.

MechAi is a web app for Supercube's mechanics. Its core is a **repair assistant** built with RAG. RAG (retrieval-augmented generation) means the app first searches Supercube's own documents for the passages that match a question, and a language model then writes an answer using only those passages. The app shows the page each step comes from, so the mechanic can always check it. More terms are explained in the [Glossary](../11%20Reference/Glossary.md).

The system is built for **every kart in the fleet**. The karts are identical, so the same logic applies to each one. Kart 07 with a worn rear axle bearing is only the example we use in demonstrations.

## The features

1. **Repair assistant.** The mechanic picks a kart and asks a question, by voice or by typing, in Dutch, French or English. The answer gives cited steps from the handbook with the page images. Safety questions follow fixed rules in code (see [Safety rules](../04%20RAG%20and%20AI/Safety%20rules.md)). When the handbook has no answer, the assistant says so instead of guessing.
2. **Kart status and service history.** Each kart has a status that matches Supercube's own system (good, diagnostic, broken, permanently broken), and a history of repairs, issues and machine alerts.
3. **Supercube connection.** MechAi reads live kart status and alerts from Supercube's API, and mechanics can mark a kart broken or repaired and run diagnostics from MechAi, the same way as in Supercube's operator app.
4. **Photo issues.** Anyone, including the operator on the floor, can report a visible problem with the camera. The issue appears in the kart history, becomes a to-do in one tap, and an "unsafe" issue takes the kart out of play.
5. **Parts stock.** Parts, stock levels and shelf locations, found by search or from a list. Taking a part lowers the stock and links it to the repair.
6. **Repair notes.** Mechanics record what they found and fixed. A note becomes a source for the assistant only after a senior mechanic approves it.
7. **To-dos and notifications.** Mechanics get to-dos from repair plans, low stock and reports, and alerts when a kart is reported unsafe, stock runs low or a note waits for approval.
8. **3D exploded view** of the kart, to show where a part sits (semester 2).

The app is designed for the workshop: mechanics have dirty hands and do not want to type. So it uses voice input, quick-pick buttons, photos instead of text, big buttons and as few taps as possible ([ADR-31 Hands-free design- voice input, quick picks, big buttons](../10%20Decision%20Log/ADR-31%20Hands-free%20design-%20voice%20input,%20quick%20picks,%20big%20buttons.md)).

Every feature has its own note under [Features](../05%20Features/Features.md). Ideas we chose not to build now are in [Parked and future ideas](../08%20Parked%20and%20Future%20Ideas/Parked%20and%20future%20ideas.md).

## Users and roles

| Role | Who | What they do in MechAi |
| --- | --- | --- |
| Operator | Receives the customers on the floor | Reports a kart that has a problem during their shift, marks it broken, sees kart status |
| Mechanic | Repairs the karts | Asks the assistant, logs repairs, reports issues, takes parts, changes kart status, runs diagnostics, writes repair notes |
| Senior mechanic | Experienced mechanic | Everything a mechanic does, plus approving repair notes and receiving alerts for unsafe karts |
| Admin | Manages the system | Staff profiles and PINs, parts list, karts and the handbook upload |

There are no personal accounts. The app is installed on shared tablets and phones; you tap your name and enter your own PIN ([Profile picker + PIN login and roles](../05%20Features/Profile%20picker%20+%20PIN%20login%20and%20roles.md)).

## Constraints

- **Safety-critical domain.** The karts have high-voltage batteries, so a wrong answer can hurt someone. Safety rules are enforced in code, not left to the AI ([ADR-30 Safety levels enforced in code](../10%20Decision%20Log/ADR-30%20Safety%20levels%20enforced%20in%20code.md)).
- **Confidential documents.** The handbook belongs to the manufacturer (OTL Italia). It never goes into git or any public place, and Supercube must agree in writing before excerpts are sent to an AI service.
- **Three languages.** Mechanics speak Dutch, French or English. The handbook is in English, so questions are translated before searching.
- **Hosting on Supercube's own servers** with Docker Compose, reachable only on the internal network ([ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](../10%20Decision%20Log/ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md)).
- **Low running cost.** The only usage cost is the OpenAI API, estimated at a few euros a month for one workshop ([Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md)).
- **Explainable to the jury.** We prefer simple, readable solutions that we can explain step by step.

## The data

- **The kart handbook:** OTL Italia "KART STORM User and Maintenance Handbook", 89 pages, English, a digital PDF with real text. The PDF page number equals the printed page number, so citations come straight from the PDF.
- **Supercube's GraphQL API:** live kart ("pod") status and alert codes.
- **Data created in MechAi:** repairs, issues and photos, stock movements, repair notes and answer feedback.
- **Not in the handbook:** Supercube's own AR parts (headset, the PC in the steering wheel, the network switch). Questions about them get "not in the handbook" until approved repair notes cover them.

## What gets graded

The school grades a full analysis plus a working prototype, the process and the presentation. Microservices are not required. The grading moments and weights are in [Planning & Deadlines](Planning%20&%20Deadlines.md).

## Timeline in short

| Period | Goal |
| --- | --- |
| 9 November to 19 December 2026 | Three sprints: a working prototype of the complete workshop flow, and the finished analysis |
| After the Christmas break | Self-evaluation with the coordinator (25%) |
| Semester 2 (7 weeks) | Remaining features, status pitch (20%), KPI check, Next Generation Showdown (process 20%, product 25%), Spread the Word (10%) |

The full plan is in [Planning & Deadlines](Planning%20&%20Deadlines.md).
