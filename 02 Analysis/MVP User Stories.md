---
tags: [analysis, user-stories]
updated: 2026-11-06
---
# MVP User Stories

Back to [Analysis](Analysis.md)

> [!NOTE]
> **MVP** here means everything in the December prototype (v0.5.0, sprints 1 to 3, 9 November to 19 December 2026). The demo follows one complete workshop story on kart 07, but every story works for every kart. Stories for semester 2 are listed at the bottom. Each story links to a requirement in [Requirements (functional & non-functional)](Requirements%20%28functional%20&%20non-functional%29.md).

## Overview

| ID | Story | Role | Priority | Sprint | Req. |
| --- | --- | --- | --- | --- | --- |
| US-01 | Sign in with my name and PIN | All | Must | 1 | FR-50 |
| US-02 | Only see what my role allows | All | Must | 1 | FR-51 |
| US-03 | Upload the handbook and make it searchable | Admin | Must | 1 | FR-20, FR-21 |
| US-04 | Ask about a kart, by voice or text, in my language | Mechanic | Must | 1 to 2 | FR-01, FR-02 |
| US-05 | Get numbered steps with a page per step | Mechanic | Must | 1 | FR-03 |
| US-06 | See the handbook page in the chat | Mechanic | Must | 2 | FR-04, FR-05 |
| US-07 | Safety level decides what I see | Mechanic | Must | 2 | FR-06, FR-07 |
| US-08 | An honest "not in the handbook" | Mechanic | Must | 2 | FR-08 |
| US-09 | Every number is checked | Mechanic | Must | 2 | FR-09 |
| US-10 | Rate an answer | Mechanic, team | Must | 3 | FR-10 |
| US-11 | Pages still shown when the AI is down | Mechanic | Should | 3 | FR-11 |
| US-12 | Report a kart problem from the floor | Operator | Must | 2 | FR-40, FR-32 |
| US-13 | See all karts and their status | All | Must | 2 | FR-30 |
| US-14 | See a kart's history and open issues | Mechanic | Must | 2 | FR-31 |
| US-15 | Mark a kart broken or repaired | Operator, mechanic | Must | 2 | FR-32 |
| US-16 | Run diagnostics on a kart | Mechanic | Should (stretch) | 3 | FR-33 |
| US-17 | Find a part and its shelf | Mechanic | Must | 3 | FR-42 |
| US-18 | Take a part so stock goes down | Mechanic | Must | 3 | FR-43 |
| US-19 | Manage parts and stock | Admin | Should | 3 | FR-44 |
| US-20 | Log a repair when I finish | Mechanic | Must | 3 | FR-31 |
| US-21 | Photo issue as a to-do and alert | Mechanic, senior | Should (stretch) | 3 | FR-41 |
| US-22 | Use it with gloves and dirty hands | All | Must | 1 to 3 | NFR usability |
| US-23 | Clear error messages with a code | All | Must | 1 to 3 | NFR reliability |
| US-24 | Every pull request is checked automatically | Team | Must | 1 | NFR maintainability |
| US-25 | Add a feature by copying a module | Team | Must | 1 | NFR maintainability |

---

## 1. Access

### US-01 Sign in with my name and PIN

**As a** user on a shared workshop tablet, **I want to** tap my name and enter my own PIN, **so that** I'm signed in fast without an account or password.

- [ ] The start screen ("Who is working?") shows every profile with name and role.
- [ ] The first time, I choose my own PIN of 4 to 6 digits; it is stored only as a hash.
- [ ] After 5 wrong PINs my profile is locked for 5 minutes; an admin can unlock it earlier and reset the PIN.
- [ ] After 30 minutes without activity I'm logged out and the app returns to the profile screen.
- [ ] A "Switch user" button is always visible.

### US-02 Only see what my role allows

**As a** user, **I want** the app to show only what my role allows, **so that** nobody approves notes or changes stock by mistake.

- [ ] Operator: report issues, see kart status, mark a kart broken.
- [ ] Mechanic: assistant, history, stock, repairs, kart status, diagnostics.
- [ ] Senior mechanic: everything a mechanic can, plus approving notes and receiving unsafe-issue alerts.
- [ ] Admin: users, parts, karts and handbook uploads.
- [ ] The backend blocks forbidden actions too, with the error code `AUTH_FORBIDDEN`.

## 2. Repair assistant

### US-03 Upload the handbook and make it searchable

**As an** admin, **I want to** upload the handbook PDF, **so that** mechanics can search it with the page numbers kept.

- [ ] I upload a PDF and see the job status (waiting, running, done, failed with an error code).
- [ ] The worker splits the text into sections and chunks, keeping section number, heading and page range.
- [ ] Every page is also saved as an image for the chat.
- [ ] Uploading a new revision only embeds the chunks that changed.
- [ ] The handbook is never committed to git.

### US-04 Ask about a kart, by voice or text, in my language

**As a** mechanic, **I want to** pick the kart and ask my question out loud in Dutch, French or English, **so that** I don't have to type or translate with dirty hands.

- [ ] I pick a kart from the list (or come from the kart's page); it stays visible at the top.
- [ ] A big microphone button records my question; the text appears so I can check it before sending.
- [ ] A Dutch or French question finds the right English pages (the question is translated into English search terms).
- [ ] The answer comes back in my language; quotes from the handbook stay in English.
- [ ] The test set has at least 5 Dutch and 5 French questions.

### US-05 Get numbered steps with a page per step

**As a** mechanic, **I want** a numbered list of steps where each step says which page it comes from, **so that** I can trust it and check it.

- [ ] Every step shows the section and page as a link.
- [ ] Page numbers come from the stored data, never typed by the model.
- [ ] Sprint 1 check: one real Dutch question finds the right page in the top 10.

### US-06 See the handbook page in the chat

**As a** mechanic, **I want to** see the real page next to the answer, **so that** I can see the drawing, table or wiring diagram it is based on.

- [ ] The cited pages appear as images under the answer.
- [ ] Tapping one opens it full screen with zoom.
- [ ] Electrical questions also show the matching wiring-diagram page.
- [ ] Images are served by the backend only after sign-in.

### US-07 Safety level decides what I see

**As a** mechanic, **I want** the app to handle dangerous situations by fixed rules, **so that** nobody gets hurt because of a bad AI answer.

- [ ] Emergency words (smoke, fire, swollen or hot battery, someone hurt) show a red STOP card with Supercube's emergency text. No AI is used.
- [ ] High-voltage questions show Supercube's fixed text and the original pages, and ask for one logged confirmation ("I have isolated the battery"). No AI-written steps.
- [ ] Bypass requests (interlock, battery management system) are refused and logged.
- [ ] When the rules and the classifier disagree, the stricter level wins.
- [ ] Every safety question in the test set lands on the right level.
- [ ] **To confirm:** the fixed texts, written or approved by Supercube.

### US-08 An honest "not in the handbook"

**As a** mechanic, **I want** the app to say when it doesn't know, **so that** I don't follow a guess.

- [ ] Below the threshold the app says "Not in the handbook, ask a senior mechanic".
- [ ] It still shows the closest pages.
- [ ] At least 4 of 5 test questions that the handbook cannot answer get this reply.

### US-09 Every number is checked

**As a** mechanic, **I want** every torque value, voltage and part number to be exactly what the handbook says, **so that** I don't overtighten a bolt or order the wrong part.

- [ ] Code checks every number against the cited pages before the answer is shown.
- [ ] If any number is not found, no steps are shown: the app shows the pages only and says why.
- [ ] 0 invented numbers in the test set.

### US-10 Rate an answer

**As a** mechanic, **I want to** give a thumbs up or down with a reason; **as the** team, **we want** to see exactly what produced the answer.

- [ ] Thumbs down asks for a quick reason (wrong page, wrong step, unsafe, other) with buttons, no typing.
- [ ] Each rating is linked to a trace: question, retrieved chunks, prompt version, model and document revision.

### US-11 Pages still shown when the AI is down

- [ ] If the AI call fails or times out, the top pages are shown with "Steps unavailable, here are the pages" and the error code.
- [ ] An admin can switch AI answers off by hand.

## 3. Fleet and Supercube

### US-12 Report a kart problem from the floor

**As an** operator, **I want to** report a problem on a kart in a few taps, **so that** the mechanics know exactly what is wrong.

- [ ] Tap the kart, pick a reason (noise, steering, brakes, battery, damage, other) and optionally say a sentence or take a photo.
- [ ] The kart is marked **BROKEN** by default, so it leaves the game; for a small issue the operator can switch this off.
- [ ] At most three taps without the voice note or photo.
- [ ] The issue shows on the kart's page with my name and the time.

### US-13 See all karts and their status

- [ ] A grid of all karts at the Brussels venue with number, photo, status and open issues.
- [ ] Status uses Supercube's four values (Good, Diagnostic, Broken, Permanently broken), shown with a word and a colour.
- [ ] In the prototype the status comes from the fake Supercube client.

### US-14 See a kart's history and open issues

- [ ] The kart page lists open issues and past repairs, newest first, with date, person, parts and photos.
- [ ] I can open the assistant for this kart in one tap.

### US-15 Mark a kart broken or repaired

**As an** operator or mechanic, **I want to** change a kart's status from MechAi, **so that** Supercube's system shows the real state.

- [ ] Operators and mechanics can mark a kart broken; mechanics, seniors and admins can mark it repaired.
- [ ] The change is logged with the person and time and sent through the `supercube` module (fake client in the prototype; stretch goal).
- [ ] If Supercube's API refuses, I see a clear message with a `SUPERCUBE_` error code and the status is not changed locally.

### US-16 Run diagnostics on a kart

**As a** mechanic, **I want to** run diagnostics from MechAi like in Supercube's operator app, **so that** I can test a kart after a repair.

- [ ] Tap Diagnostics, then choose Pitlane, Cruise, Boost, High boost or High brake.
- [ ] A big Stop button ends it.
- [ ] No extra PIN; every start and stop is logged with the person and time.
- [ ] Uses the fake client until Supercube gives API access.

## 4. Stock and repairs

### US-17 Find a part and its shelf

- [ ] Search parts by name or part number, or browse the list.
- [ ] Each part shows stock and shelf; parts at or below their minimum are marked.

### US-18 Take a part so stock goes down

- [ ] "Take" lowers the stock and links the part to the kart and the repair.
- [ ] Stock never goes below zero (`INVENTORY_STOCK_NEGATIVE`).
- [ ] A double tap is not counted twice (each request has its own id).

### US-19 Manage parts and stock (admin)

- [ ] Add, edit and archive parts; correct a count (logged); set a minimum level.

### US-20 Log a repair when I finish

- [ ] Log what I did with quick picks and voice; parts I took are filled in.
- [ ] If the repair fixes an open issue, I can close it, with an optional "after" photo.
- [ ] I can mark the kart repaired in the same flow.

### US-21 Photo issue as a to-do and alert (stretch goal)

- [ ] One tap turns an issue into a to-do; closing the to-do closes the issue.
- [ ] "Kart unsafe" alerts the senior mechanics and marks the kart broken.

## 5. Platform

### US-22 Use it with gloves and dirty hands

- [ ] Installable PWA on Android and iOS; tablet is the main layout.
- [ ] Touch targets at least 56 px; a microphone button wherever text is asked.
- [ ] High contrast, readable in a bright workshop.
- [ ] **To confirm:** which devices the workshop uses.

### US-23 Clear error messages with a code

- [ ] Every error shows a friendly message in my language, the error code and a reference id.
- [ ] The reference id lets the team find the matching log line.

### US-24 Every pull request is checked automatically

- [ ] Each pull request runs formatting and lint checks, tests, the retrieval evaluation on a small fake manual and a Docker build.
- [ ] CI fails if recall on the fake manual drops below its baseline. The real evaluation runs on the server.

### US-25 Add a feature by copying a module

- [ ] Backend modules all have `models.py`, `schemas.py`, `service.py`, `router.py`, `errors.py` and a README.
- [ ] Frontend features all have `api.ts`, `pages/` and `components/`.
- [ ] Shared code lives only in `core/` and `components/ui/`.

---

## Semester 2 stories

- Repair notes with senior approval, then searched by the assistant.
- To-dos per kart and notifications.
- Step-by-step mode with read-aloud.
- Live status and alerts from Supercube's API (once access is granted).
- Photo questions in the chat; stock shown in answers.
- Relevance check and other retrieval upgrades, each kept only if the tests improve.
- 3D exploded view of the kart.
