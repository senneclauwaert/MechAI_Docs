---
tags: [analysis]
updated: 2026-11-06
---
# User & Stakeholder Analysis

Back to [Analysis](Analysis.md)

## Personas

> [!NOTE]
> These personas are based on Senne's own experience as a mechanic at Supercube. They are validated with short interviews with colleagues (see the last section).

### Operator

- **Role:** receives the customers on the gaming floor and runs the sessions.
- **Goals:** notice quickly when a kart misbehaves, take it out of play, and pass the problem on to the mechanics without leaving the floor for long.
- **Frustrations:** problems passed on by word of mouth get forgotten or lose detail; no way to see whether a kart is fixed yet.
- **In MechAi:** reports an issue on a kart (voice, quick-pick buttons or a photo), marks the kart broken, sees the status of every kart.
- **Devices:** a phone or a tablet at the desk. Little time, so everything must be fast.

### Mechanic

- **Goals:** get a broken kart back on the floor as fast as possible, safely; find the right procedure, torque value or part without searching the handbook; know what was already done to this kart; know whether the part is in stock.
- **Frustrations:** the handbook is slow to search and in English; knowledge sits with colleagues who are not always on shift; high-voltage work needs certainty, not a guess; typing on a tablet with dirty hands is not practical.
- **In MechAi:** asks the assistant by voice, follows the steps one by one, takes parts from stock, logs the repair, changes the kart status and runs diagnostics, writes repair notes.
- **Devices:** a shared workshop tablet and a phone; often with gloves or dirty hands, in a noisy, bright space.
- **Languages:** Dutch, French or English.

### Senior mechanic

- **Goals:** keep repairs safe and consistent; pass on experience.
- **Frustrations:** answering the same questions again and again; no record of how a recurring fault was fixed last time.
- **In MechAi:** everything a mechanic does, plus approving repair notes and receiving alerts when a kart is reported unsafe. Reviews the safety answers before the Showdown.

### Admin

- **Goals:** keep the system and its data correct.
- **In MechAi:** manages staff profiles and PIN resets, the parts list and stock corrections, the kart list, and uploads new handbook revisions. **To confirm:** whether this is a separate person or the workshop manager.

## Stakeholders

| Stakeholder | Interest | Influence | What we need from them |
| --- | --- | --- | --- |
| Mechanics and operators | Faster, safer repairs; less hassle | Medium | Real test questions, feedback on the prototype |
| Senior mechanic | Safety and quality | High | Approving notes, the safety review |
| Supercube management | Less downtime, low cost, data stays private | High | Permissions, the fixed safety texts, a server, API access ([Questions for Supercube](../01%20Project/Questions%20for%20Supercube.md)) |
| Supercube IT | A system that is easy to run and back up | Medium | Server, internal hostname and HTTPS certificate, backups |
| OTL Italia (kart manufacturer) | Owns the handbook (copyright) | Low | Indirectly, through Supercube's permission |
| OpenAI (AI service) | Provides the language model, embeddings and speech-to-text | Low | A paid API account; data terms checked before go-live |
| Senne and Nehad | A working product and a strong grade | High | A clear role split |
| Erasmushogeschool Brussel (coach and jury) | A complete analysis and a product the team can explain | High | Exact deadlines |
| Customers (drivers) | Indirect: more karts available, safer karts | Low | Nothing; they don't use the app |

## Interviews and observations

- **Done so far:** Senne's own experience as a mechanic; photos of a real Supercube kart; the handbook and the API schema received from Supercube.
- **To do:**
  - [ ] Ask three mechanics for the last five problems they had to look up, and which page of the handbook answered each one. This starts the test set.
  - [ ] Ask an operator how a kart problem is passed on today.
  - [ ] Watch one real repair from fault to fix and time each step (the baseline for the KPI "time to find a procedure").
  - [ ] Test the prototype with two or three mechanics and an operator, and note where they get stuck.
