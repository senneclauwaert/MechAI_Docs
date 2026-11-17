---
tags: [analysis, requirements]
updated: 2026-11-17
---
# Requirements (functional & non-functional)

Back to [Analysis](Analysis.md)

> [!TIP]
> **MoSCoW** ranks each requirement: **Must** (the prototype fails without it), **Should** (important, planned), **Could** (if time allows), **Won't** (not in this project). **When** says when it is built: **Dec** = the December prototype (v0.5.0, sprints 1 to 3), **S2** = semester 2 (February to March 2027, 7 weeks).

## Functional requirements

### Repair assistant

| ID | Requirement | Priority | When |
| --- | --- | --- | --- |
| FR-01 | A mechanic picks a kart and asks a repair question in Dutch, French or English. | Must | Dec |
| FR-02 | A question can be spoken instead of typed (speech-to-text). | Must | Dec |
| FR-03 | The answer is a numbered list of steps built only from the retrieved handbook sections, each step citing its page. | Must | Dec |
| FR-04 | The cited handbook pages are shown as images in the chat; tapping one opens it full screen with zoom. | Must | Dec |
| FR-05 | Electrical questions show the matching wiring-diagram page as an image. | Should | Dec |
| FR-06 | Every question gets a safety level in code. **Emergency** (smoke, fire, swollen or hot battery, someone hurt): a STOP card, no AI. **High voltage** (battery, charger, motor controller, HV wiring): Supercube's fixed text and the original pages, plus a logged confirmation, no AI-written steps. **Normal:** cited steps. The stricter level always wins. | Must | Dec |
| FR-07 | Requests to bypass an interlock or the battery management system are refused and logged. | Must | Dec |
| FR-08 | When the sources are too weak, the assistant says "Not in the handbook, ask a senior mechanic" and shows the closest pages. | Must | Dec |
| FR-09 | Every number (torque, voltage, part number) in an answer must appear on a cited page; code checks this before the answer is shown. | Must | Dec |
| FR-10 | Thumbs up or down with a reason on every answer, linked to a trace. | Must | Dec |
| FR-11 | Retrieval-only mode: when the AI service is down, the relevant pages are shown without generated steps. | Should | Dec |
| FR-12 | Step-by-step mode: one step per screen with big Next and Back buttons; optional read-aloud. | Should | S2 |
| FR-13 | Questions that are not about kart repair get a short, polite refusal. | Should | S2 |
| FR-14 | The answer shows whether the parts it mentions are in stock. | Could | S2 |
| FR-15 | A photo can be added to a question ("what is this part?"). | Could | S2 |

### Handbook and repair notes

| ID | Requirement | Priority | When |
| --- | --- | --- | --- |
| FR-20 | An admin uploads the handbook PDF; the worker reads it (no OCR needed), splits it into sections and chunks, creates embeddings and renders every page as an image. | Must | Dec |
| FR-21 | Each upload is stored as a document revision. Only new or changed chunks get new embeddings (a content hash decides). | Must | Dec |
| FR-22 | Each answer trace records which document revision it used. | Should | Dec |
| FR-23 | A mechanic writes a repair note: kart, symptom, cause, fix, parts, photos. | Should | S2 |
| FR-24 | A senior mechanic approves or rejects a note. Only approved notes are searched; they rank below the handbook and are never a source for a safety step. Editing an approved note removes its approval. | Should | S2 |

### Fleet and Supercube integration

| ID | Requirement | Priority | When |
| --- | --- | --- | --- |
| FR-30 | Kart list for the Brussels venue with each kart's status (Supercube's values: Good, Diagnostic, Broken, Permanently broken) and the number of open issues. A venue field allows more venues later. | Must | Dec |
| FR-31 | Service history per kart: repairs, issues and photos with date, person and parts. | Must | Dec |
| FR-32 | Every signed-in user except the operator can mark a kart repaired; operators and mechanics can mark a kart broken. The change is logged with the person and time, and sent to Supercube's API through the `supercube` module. | Must | Dec (in MechAi); Supercube connection: stretch, fake client |
| FR-33 | A mechanic runs diagnostics on a kart: tap Diagnostics, choose Pitlane, Cruise, Boost, High boost or High brake; Stop ends it. Same flow as Supercube's operator app, no extra PIN, plus a "nobody at the kart" confirmation, an automatic stop after 60 seconds without a command, and a block while someone else has an open repair on that kart. Every start and stop is logged. | Should | Dec stretch (fake client) |
| FR-34 | Live kart status and alerts are read from Supercube's API. | Should | S2 (after access) |

### Issues, stock and tasks

| ID | Requirement | Priority | When |
| --- | --- | --- | --- |
| FR-40 | The operator or a mechanic reports an issue on a kart: quick-pick reason, optional voice description, optional photos, severity (low, high, kart unsafe). | Must | Dec |
| FR-41 | An issue shows in the kart history and can become a to-do in one tap. "Kart unsafe" alerts the senior mechanics and marks the kart broken. An optional "after" photo closes it. | Should | Dec (stretch) |
| FR-42 | Parts list with stock and shelf, searchable by name or part number. | Must | Dec |
| FR-43 | Taking a part lowers the stock in one transaction; stock never goes below zero; a repeated tap is not counted twice. | Must | Dec |
| FR-44 | An admin adds parts, corrects stock (logged) and sets a minimum level. | Should | Dec |
| FR-45 | To-dos per kart, optionally assigned to a person. | Should | S2 |
| FR-46 | Notifications in the app: unsafe issue, note to approve, low stock, task assigned. | Should | S2 |
| FR-47 | 3D exploded view of the kart with the faulty part highlighted. | Could | S2 |

### Access

| ID | Requirement | Priority | When |
| --- | --- | --- | --- |
| FR-50 | Sign-in without accounts: tap your name, enter your own PIN (4 to 6 digits). 5 wrong tries lock the profile for 5 minutes; an admin can reset it. Logout after 30 minutes without activity. | Must | Dec |
| FR-51 | Four roles, checked by the backend on every request: **operator** (report issues, see status, mark a kart broken), **mechanic** (assistant, history, stock, repairs, status, diagnostics, notes), **senior mechanic** (mechanic plus approving notes and unsafe-issue alerts), **admin** (users, parts, karts, handbook uploads). | Must | Dec |

### Won't (this project)

QR codes; an outside login service; repair videos turned into steps; camera stock counting; predictive maintenance; public internet access; customer-facing features.

## Non-functional requirements

### Accuracy and safety (most important)

- Retrieval quality is measured with a test set of 30 to 50 real questions: recall@10, MRR, citation accuracy, invented numbers, correct refusals and safety level.
- CI checks search quality on a small fake manual (the handbook is never in git); the real evaluation runs on the server against the real index, per handbook version.
- The AI never writes high-voltage or emergency steps. Safety texts come from Supercube.
- Handbook text and repair notes are passed to the model as data, never as instructions (protection against prompt injection).

### Usability (dirty hands, gloves, noise)

- Voice input on every place where text is asked.
- Quick-pick buttons instead of free text where possible; a photo instead of a description.
- Touch targets of at least 56 px; at most three taps for the main tasks.
- Readable in a bright workshop: white background, high contrast, status shown with a word and a colour.
- Installable PWA; the workshop tablet is the main layout, phones work too.
- Dutch, French and English in the interface.

### Performance

- A repair answer starts appearing within about 10 seconds; search results alone within 2 seconds. **To confirm** after the first measurement.
- Photos are resized on the device before upload.

### Security and privacy

- MechAi is only reachable on Supercube's internal network, over HTTPS with a certificate from Supercube IT.
- PINs are stored only as an Argon2 hash. The session lives in an http-only cookie. PIN attempts are rate limited.
- Secrets live in an `.env` file or Docker secrets on the server, never in git.
- Photos and page images are served only through the backend, after sign-in.
- Only the handbook sections needed for one question are sent to the Mistral API, after Supercube's written OK. Traces stay in our own database.
- The manufacturer's handbook never goes into git or any public place.

### Reliability and error handling

- Every error has the same shape: a code, a message and a reference id. Each module has its own code prefix (for example `INVENTORY_STOCK_NEGATIVE`). The interface shows a friendly message in the user's language with the code. See [Error handling](../03%20Architecture/Error%20handling.md).
- Background jobs retry safely and record their last error.
- A health endpoint, restart policies and a nightly backup of the database and files.

### Cost

- The Mistral API is the only running cost: Mistral Small and `mistral-embed` (about $5 to $8 a month for 3,000 questions). A monthly budget limit, a question limit per user, a daily cap and a switch that turns AI answers off.
- Hosting runs on Supercube's own server, so there is no cloud bill.

### Maintainability

- One modular backend; every module has the same files (`models.py`, `schemas.py`, `service.py`, `router.py`, `errors.py`, README).
- Readable, not duplicated, automatically formatted: ruff for Python, Prettier and ESLint for TypeScript, run by pre-commit and CI.
- Prompts, migrations and the test set are versioned in git; each answer logs the prompt version, model and document revision.

### Scalability

- A handful of users at one venue: one backend instance and one worker are enough.
- Strict module boundaries, so a module could become a separate service later if ever needed.
