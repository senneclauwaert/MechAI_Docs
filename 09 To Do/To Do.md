---
tags: [todo, index]
updated: 2026-11-17
---
# To Do

Back to [Final Work Hub](../Final%20Work%20Hub.md) · Plan: [Planning & Deadlines](../01%20Project/Planning%20&%20Deadlines.md)

All tasks in one table per sprint. When a task changes, update its **Status** (To do, In progress, Review, Done) and, if useful, the **Who** column. Owners are filled in once the team agrees the role split ([Team & Agreements](../01%20Project/Team%20&%20Agreements.md)). The code tasks will move to GitHub issues once the code repository exists.

## Now (before sprint 1)

| ID | Task | Who | Status | Due |
| --- | --- | --- | --- | --- |
| T-01 | Send [Questions for Supercube](../01%20Project/Questions%20for%20Supercube.md) to Supercube, including the permissions checklist to sign | Senne | To do | 9 Nov 2026 |
| T-02 | Ask Supercube IT for a server, an internal hostname and an HTTPS certificate | Senne | To do | 9 Nov 2026 |
| T-03 | Create the private documentation repository, push this vault, invite Nehad, the coach and Supercube (read access) | Senne | To do | 9 Nov 2026 |
| T-04 | Agree the role split, the Definition of Done and the team agreements | Senne, Nehad | To do | 9 Nov 2026 |
| T-05 | Confirm the KPI targets | Senne, Nehad | To do | 9 Nov 2026 |
| T-06 | Ask the school whether Supercube must be approved as the client, and for the exact dates | Senne | To do | 13 Nov 2026 |
| T-07 | Create a Mistral API account (La Plateforme) with a monthly budget limit (decide whose account it is; see [Open questions](../01%20Project/Open%20questions.md)) | | To do | 9 Nov 2026 |

## Sprint 1: skeleton and baseline assistant (9 – 22 Nov 2026)

| ID | Task | Who | Status |
| --- | --- | --- | --- |
| T-10 | Private code repository with the monorepo layout, the module template, README, `.env.example`, pre-commit (ruff, Prettier, ESLint, gitleaks) | | To do |
| T-11 | Docker Compose with `db`, `api`, `worker`, `web`; FastAPI skeleton with `/health`; first Alembic migration | | To do |
| T-12 | `core/errors.py`, the error shape and the first module error codes; frontend error helper with translations | | To do |
| T-13 | CI workflow: formatting, lint, types, tests, Docker build on every pull request | | To do |
| T-14 | `auth` module: profile picker, PIN login, four roles, lockout, 30-minute idle logout | | To do |
| T-15 | `storage` module: `save_file()`, `open_file()`, photo resizing | | To do |
| T-16 | Handbook ingestion in the worker: Docling (no OCR), sections, chunks with context headers, content hash, embeddings, page images | | To do |
| T-17 | Write the first 5 test questions (15 by the end of sprint 2) with expected pages from the real handbook (including Dutch and French) and `eval/run_eval.py` (recall@5, recall@10, MRR) | | To do |
| T-18 | Baseline assistant: English translation, hybrid search with RRF, parent sections, cited answer, refusal threshold | | To do |
| T-19 | Bare web page: pick a kart, ask a question, see the cited answer. Tag `v0.1.0` | | To do |

## Sprint 2: the workshop flow (23 Nov – 6 Dec 2026)

| ID | Task | Who | Status |
| --- | --- | --- | --- |
| T-20 | `fleet` module: kart grid and kart page with history, for every kart (seed data for the Brussels fleet) | | To do |
| T-21 | `issues` module: operator issue report with quick picks, voice and an optional photo; mark the kart broken | | To do |
| T-22 | Safety levels: word lists, the AI flag, the STOP card, the high-voltage screen with the logged confirmation (placeholder texts until Supercube's arrive) | | To do |
| T-23 | Page images in the chat, tap to zoom; wiring-diagram page for electrical questions | | To do |
| T-24 | Voice input: microphone button and `POST /assistant/transcribe` | | To do |
| T-25 | Number and citation verification in code | | To do |
| T-26 | Grow the test set to 30 questions; one measured improvement | | To do |

## Sprint 3: demo-ready (7 – 19 Dec 2026)

| ID | Task | Who | Status |
| --- | --- | --- | --- |
| T-30 | `inventory` module: parts list, search, "Take part" with a request id, admin corrections | | To do |
| T-31 | Log a repair: quick picks, voice, parts taken, close the issue, mark the kart repaired | | To do |
| T-32 | Answer feedback and traces | | To do |
| T-33 | Retrieval-only mode and the admin AI switch | | To do |
| T-34 | Hands-free pass on every screen (56 px targets, at most three taps) | | To do |
| T-35 | Stretch: `supercube` module with the fake client (status and diagnostics) | | To do |
| T-36 | Stretch: photo issues as a to-do and unsafe alert | | To do |
| T-37 | Finish the analysis document; record the demo video. Tag `v0.5.0` | | To do |

## Documentation and design

| ID | Task | Who | Status |
| --- | --- | --- | --- |
| T-40 | Update the HTML prototype for the 6 November decisions (operator flow, Diagnostics, four kart statuses, safety levels, microphone button, real handbook sections; QR buttons and the Gent venue removed) and restyle it in light blue | Senne | Done |
| T-41 | Mark the Figma file as history only (the HTML prototype is the reference and has a new look) | | To do |
| T-42 | Write the emergency and high-voltage texts with Supercube | Senne | Waiting for Supercube |
| T-43 | Nehad reads and confirms ADR-1 to ADR-36; add a "Decided by" field to each ADR | Senne, Nehad | To do |
| T-44 | Check EhB's rules on AI use and add a short AI-use statement to the shared docs | Senne | To do |
| T-45 | Put the prototype HTML file in the docs repository so readers don't need the claude.ai link (it contains no handbook text) | Senne | To do |
| T-46 | Write the small fake manual for the CI evaluation and cache the question embeddings | | To do |

## Done

| ID | Task | Done on |
| --- | --- | --- |
| — | Get the handbook as a PDF | 6 Nov 2026 |
| — | Review every decision and clean up this vault | 6 Nov 2026 |
| — | Decide on GraphQL and the Supercube API | 6 Nov 2026 |

> [!NOTE]
> The task list of 16 October (photographing pages, testing Azure OpenAI on a student subscription, updating the LangChain starter, updating the FigJam board) was closed on 6 November 2026 because those tasks no longer apply.
