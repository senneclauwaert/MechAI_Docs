---
tags: [project, planning]
updated: 2026-11-06
---
# Planning & Deadlines

Back to [Final Work Hub](../Final%20Work%20Hub.md)

This plan follows the official Final Work timeline of the school (day track). We work in sprints of about two weeks; every sprint ends with something we can demonstrate. The tasks are in [To Do](../09%20To%20Do/To%20Do.md) and the features in [Features](../05%20Features/Features.md). Exact calendar dates of the school moments are still to confirm.

## School timeline and grading

| Moment | What happens | Weight |
| --- | --- | --- |
| Semester 1, weeks 1-4 | Course information, forming the group, brainstorm, presenting our WHY, planning, proposal (deadline 30 October 2026) | |
| Semester 1, week 5 until the Christmas break | Define and build the analysis and the prototype | |
| After the Christmas break | Self-evaluation (end product and competences) in a conversation with the coordinator | **25%** |
| Semester 2, weeks 1-2 | Continue building the product | |
| Semester 2, week 3 | Status pitch to the teachers, using the skills from the communication courses | **20%** |
| Semester 2, week 4 | Future skills: self-evaluation, evaluate our KPIs, decide how to adjust | |
| Semester 2, week 5 | Work week | |
| Semester 2, week 6 | Next Generation Showdown: final evaluation of the process and the product, presented with the Steve Jobs checklist | **Process 20%, product 25%** |
| Semester 2, week 7 | Spread The Word: show the work to the world, for example with a product website, a flyer or a video | **10%** |

## Semester 1: prototype and analysis

| Sprint | Dates | Goal and demo at the end |
| --- | --- | --- |
| **Sprint 1: skeleton and baseline assistant** | 9 – 22 Nov 2026 | Code repository with the module template, linting and CI. Docker Compose with PostgreSQL and pgvector. PIN login with the four roles. Ingestion working with Docling on a few test pages (sections, chunks, page images); the whole handbook only after Supercube's written OK. Baseline assistant: English translation of the question, hybrid search, whole sections, cited answer and "not in the handbook". The first 5 real test questions and the evaluation script. Email to Supercube with our questions. Tag `v0.1.0` |
| **Sprint 2: the workshop flow** | 23 Nov – 6 Dec 2026 | Kart list and kart page with history for every kart. Operator issue log and kart status. The whole handbook ingested (once Supercube's OK is in). Test set grown to 15 questions. Safety levels with fixed texts. Page images in the chat. Voice input. One measured improvement to the assistant |
| **Sprint 3: demo-ready** | 7 – 19 Dec 2026 | Recording a repair and taking a part from stock. Answer feedback and traces. Hands-free and big-button pass on every screen. Finished analysis document. Recorded demo video. Stretch goals if there is time: photo issues, Supercube status and diagnostics with fake data. Tag `v0.5.0` |

The task-level sprint numbers live in [To Do](../09%20To%20Do/To%20Do.md); this table is the summary.

**The December demo** is described only here; other notes link to it. It shows one complete workshop flow, using kart 07 as the example. The system itself works for every kart.

1. Log in with a PIN (operator, mechanic, senior).
2. The operator reports "kart 07 makes a grinding noise at the rear" and marks it broken.
3. A mechanic opens kart 07 and sees its history and the open issue.
4. The mechanic asks the assistant out loud, in Dutch. The answer cites the real handbook (4.5.16 Rear axle and bearings, page 17; 5.3 Rear mechanical section, pages 38-42; 5.6.2 Replacing the drive shaft bearings, page 48) with the page images. A high-voltage question shows the safety level instead, and an unrelated question gets "not in the handbook".
5. The mechanic records the repair and takes the bearing from stock; the stock goes down.
6. The mechanic rates the answer, and we show the test scores of the baseline against one improvement.

## Semester 2: completion

| Week | Goal |
| --- | --- |
| Weeks 1-2 | Repair notes as a source for the assistant, to-dos and notifications, photo issues (if not done in December), the real Supercube connection (once access is granted), the retrieval improvements from ADR-22 |
| Week 3 | Status pitch (20%) |
| Week 4 | KPI check and adjustment (see below) |
| Week 5 | 3D exploded view, testing in the real workshop, safety review with a senior mechanic, fixes |
| Week 6 | Next Generation Showdown. Tag `v1.0.0`, demo script and a recorded backup video |
| Week 7 | Spread The Word: a product website and a short video |

## KPIs (proposed, to confirm by the team)

KPIs (key performance indicators) are the measurable goals we evaluate in week 4 of semester 2.

| KPI | Target (proposal) |
| --- | --- |
| The right handbook page is in the top 10 search results (recall@10) | At least 80% of the test questions |
| Invented numbers in answers (torque, sizes, part numbers) | 0 in the test set |
| Correct "not in the handbook" on questions the handbook cannot answer | At least 4 out of 5 |
| Safety questions handled at the right safety level | 100% of the safety test questions |
| Time until the answer appears | About 10 seconds or less |
| Time for a mechanic to find a repair procedure, with and without MechAi | Measured in the workshop; MechAi should be clearly faster |
| Mechanics who tried the app in the workshop and gave feedback | At least 3 |

## Rules

- **Scope freeze:** nothing from semester 2 starts before the December demo works.
- **Measure first:** every change to the assistant is measured on the test set ([Optimization playbook](../04%20RAG%20and%20AI/Optimization%20playbook.md)).
- **Not built in this project:** QR codes, an outside login service, repair videos (parked), camera stock counting and predictive maintenance. See [Parked and future ideas](../08%20Parked%20and%20Future%20Ideas/Parked%20and%20future%20ideas.md).

> [!NOTE]
> The earlier plan (16 October) had four sprints from 19 October to 13 December, an Azure deployment in sprint 4 and the jury estimated around April 2027. It was replaced on 6 November 2026 by this plan, which follows the school timeline, starts building on 9 November and runs on Supercube's own servers. See [Superseded decisions](../10%20Decision%20Log/Superseded%20decisions.md).
