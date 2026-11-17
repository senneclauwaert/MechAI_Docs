---
tags: [project, open]
updated: 2026-11-17
---
# Open questions

Back to [Final Work Hub](../Final%20Work%20Hub.md)

This note collects the questions that are still open for the school and for the team, plus product details we will settle while building. Questions for Supercube are in a separate note that can be sent to them: [Questions for Supercube](Questions%20for%20Supercube.md). When a question is answered, tick it and write the answer and the date next to it. A big answer also becomes a decision in the [Decision Log](../10%20Decision%20Log/Decision%20Log.md).

## 1. For the school

- [ ] What are the exact dates of the self-evaluation after Christmas, the status pitch (semester 2, week 3) and the Next Generation Showdown (semester 2, week 6)?
- [ ] Does Supercube need to be approved as the client of the Final Work?

## 2. For the team

- [ ] How do Senne and Nehad split the roles? See [Team & Agreements](Team%20&%20Agreements.md).
- [ ] Agree the Definition of Done and the team agreements.
- [ ] Confirm the KPI targets in [Planning & Deadlines](Planning%20&%20Deadlines.md).

## 3. Product details (defaults are fine unless someone objects)

These details do not block the start of the build. Where a default is given, we build that unless the team or Supercube decides otherwise.

**Login and roles**
- [ ] Who creates a new profile? *Default: only an admin.*
- [ ] PIN length? *Default: 4 to 6 digits, chosen by the person; an admin resets a forgotten PIN.*
- [ ] Is the 30-minute idle logout right for a busy workshop? *Default: 30 minutes.*
- [ ] Can the operator also use the repair assistant? *Default: no, the operator reports issues and sees kart status.*

**Repair assistant**
- [ ] Should the answer come back in the language of the question? *Default: yes; quotes from the handbook stay in English.*
- [ ] Is a chat history per kart useful ("what did someone ask about kart 07 yesterday?")? *Default: yes, recent questions per kart.*
- [ ] Should the assistant also answer stock and history questions ("how many bearings are left?")? *Default: not in the prototype; a semester 2 idea.*

**Karts and history**
- [ ] What must one history entry hold? *Default: date, who, what was done, parts used, photos, link to the issue or to-do.*
- [ ] Are there regular services (for example every X driving hours) that MechAi should track? *Default: repairs only in the prototype.*

**Stock**
- [ ] Who may add stock or correct counts? *Default: admins; every correction is logged.*

**To-dos and notifications**
- [ ] Can a to-do be assigned to a person, or only to a kart? *Default: both, person optional.*
- [ ] Only a badge in the app, or real push notifications? *Default: a badge in the app; push notifications on iPhone PWAs are limited.*

**Photo issues**
- [ ] Maximum number of photos per issue, and is an "after" photo required when closing? *Default: up to 6 photos; the "after" photo is optional.*

**3D view**
- [ ] Is a simplified block model enough, or is a realistic model expected? Depends on whether CAD files exist ([Questions for Supercube](Questions%20for%20Supercube.md)).

## Answered on 6 November 2026

- **Handbook:** a digital PDF in English (OTL Storm handbook, 89 pages).
- **Hosting:** Supercube's own servers with Docker Compose, internal network only; no Azure.
- **AI provider:** the Mistral API (decided 17 November 2026); other models are tested later, and Supercube may still bring its own account.
- **Stack:** Python with FastAPI; React, TypeScript and Vite as a PWA; plain Python RAG code.
- **Safety:** three safety levels enforced in code; the AI never writes high-voltage or emergency steps.
- **Retrieval:** simple baseline first, with translation; extra steps only when the tests show they help.
- **Roles:** operator, mechanic, senior mechanic, admin.
- **Diagnostics and status changes:** available to every mechanic, like Supercube's operator app.
- **December scope:** one complete workshop flow for every kart; 3D view in semester 2.
- **Venue:** Brussels only for now.

All of these are recorded in the [Decision Log](../10%20Decision%20Log/Decision%20Log.md).

## Raised by the review of 6 November 2026

- [ ] **Mistral account:** whose account is it, who pays, and what happens to it after the project?
- [ ] **Code ownership:** who owns the code, under which licence, and who maintains it after June 2027?
- [ ] **Demo data:** where do the kart list and parts list for sprints 2 and 3 come from? How are repair history and stock tracked today?
- [ ] **Sharing the handbook with Nehad:** through which private channel, and with Supercube's OK?
- [ ] **Safety texts:** in which languages do the fixed texts come? Until Supercube's texts arrive (T-42), the demo texts are labelled as placeholders on screen.
- [ ] **Guest Wi-Fi:** is the customers' Wi-Fi a separate network from the internal one?
- [ ] **Supercube's API schema:** may the docs repository, which teachers can read, describe Supercube's GraphQL schema?
- [ ] **Product name:** a competitor is called MECH AI. Keep "MechAi" or pick another name before Spread the Word?
