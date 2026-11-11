---
tags: [analysis, index]
updated: 2026-11-06
---
# Analysis

Back to [Final Work Hub](../Final%20Work%20Hub.md)

This folder holds the analysis of MechAi: the problem, the users, the requirements, the market and the technical choices. It reflects the decisions confirmed on 6 November 2026. Statements marked **To confirm** still need an answer from Supercube or the school.

## Problem statement

**Supercube** runs AR karting (drivers wear a headset and race on a "gaming floor") with a fleet of identical single-seat electric karts. The mechanics keep that fleet running between sessions. This project covers the Brussels venue.

**The problem:** when a kart breaks, a mechanic needs the right repair information fast, and today that information is hard to reach.

- **One handbook, hard to search.** The only written source is the manufacturer's handbook (OTL Italia, "KART STORM User and Maintenance Handbook", 89 pages, English). Finding the right section during a repair takes time, and it is not in the mechanics' own language.
- **Experience lives in people's heads.** What a mechanic learned fixing one kart is not written down, so the next mechanic with the same fault starts from zero.
- **Safety is critical.** The karts run on high-voltage batteries and have a motor controller. A wrong step can hurt someone, so guessing is not acceptable.
- **Information is spread out.** Kart status lives in Supercube's own system, while repair history, spare-part stock, visible damage and open jobs are not recorded in one place. **To confirm:** how repair history and stock are tracked today.
- **The workshop is a hard place to type.** Mechanics work with dirty hands or gloves, so any tool that needs a lot of typing will not be used.

**How they handle it now:** a mechanic leafs through the handbook, asks a more experienced colleague, or relies on memory and trial and error. Downtime costs the business directly: a kart off the floor is a kart nobody can drive.

**The idea in one sentence:** a web app where a mechanic picks a kart, asks a question out loud, and gets the steps from the handbook with the page to prove it, together with the kart's status and history, photo issues, stock and to-dos.

> [!NOTE]
> **RAG (retrieval-augmented generation)** is the technique behind the repair assistant. First the app searches the handbook for the passages that match the question. Then a language model writes an answer using only those passages, and shows which page each step comes from. The model does not answer from its own general knowledge.

## Goals and scope

**In scope:**

- **Repair assistant** over the handbook: questions by voice or text in Dutch, French or English; cited steps with page images; fixed safety rules in code; "not in the handbook" when the sources are weak.
- **Handbook ingestion:** an admin uploads the PDF; the background worker turns it into searchable sections and page images.
- **Kart status and service history** for every kart, with the status shared with Supercube's own system.
- **Supercube integration:** read kart status and alerts; mark a kart broken or repaired; run diagnostics.
- **Operator issue log and photo issues:** report a problem on a kart, with photos, from the floor or the workshop.
- **Parts stock:** parts, stock and shelf, found by search or from a list; taking a part lowers the stock.
- **Repair notes** approved by a senior mechanic, as an extra source for the assistant.
- **To-dos and notifications.**
- **3D exploded view** of the kart (semester 2).
- **Login with a profile picker and personal PIN**, four roles (operator, mechanic, senior mechanic, admin).
- **Hosting on Supercube's own servers** with Docker Compose, CI, an evaluation with a test set, and this analysis.
- **Simple, modular code** with clear error codes.

**Out of scope:**

- Microservices (one modular backend plus one worker is enough).
- Public internet access to MechAi: it is only reachable on Supercube's internal network.
- Cloud hosting (Azure or similar) and local AI models on our own hardware.
- QR codes and an outside login service.
- Repair videos (parked), camera stock counting and predictive maintenance.
- Customer-facing features (bookings, timing, the AR game itself).
- Publishing the handbook: it stays private.

## Success criteria

- [ ] A mechanic solves a real kart problem with MechAi and the right handbook page is cited.
- [ ] The right page is in the top 10 search results for at least 80% of the test questions (recall@10 ≥ 0.8). **To confirm** after the first measurement.
- [ ] Every number in an answer appears on the cited page: 0 invented numbers in the test set.
- [ ] The assistant says "not in the handbook" on at least 4 of 5 questions the handbook cannot answer.
- [ ] Every safety question in the test set lands on the right safety level, and no AI-written steps appear for high-voltage or emergency questions.
- [ ] A spoken question in Dutch gives the same answer as the typed question.
- [ ] The operator can report a kart problem in three taps or fewer, plus voice or a photo.
- [ ] An answer appears within about 10 seconds on the workshop Wi-Fi. **To confirm.**
- [ ] A senior mechanic has reviewed the safety answers before the Showdown.
- [ ] The team can explain every step of the pipeline, with before-and-after evaluation numbers.

## Analysis notes

- [User & Stakeholder Analysis](User%20&%20Stakeholder%20Analysis.md)
- [Current Situation (As-Is) vs. Future (To-Be)](Current%20Situation%20%28As-Is%29%20vs.%20Future%20%28To-Be%29.md)
- [Requirements (functional & non-functional)](Requirements%20%28functional%20&%20non-functional%29.md)
- [MVP User Stories](MVP%20User%20Stories.md)
- [Market & Competitor Analysis](Market%20&%20Competitor%20Analysis.md)
- [Technical Analysis (RAG, LLM & stack)](Technical%20Analysis%20%28RAG,%20LLM%20&%20stack%29.md)
