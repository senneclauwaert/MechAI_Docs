---
tags: [architecture, dev]
updated: 2026-11-06
---
# Repo & dev setup

Back to [Architecture](Architecture.md)

> [!WARNING]
> The code repository is private on GitHub. It never contains the manufacturer's handbook, page images, photos or keys. The handbook is uploaded through the admin screen on each environment.

## Repository layout

```txt
mechai/
├─ backend/
│  ├─ app/
│  │  ├─ main.py            # FastAPI app, registers one router per module
│  │  ├─ worker.py          # job loop (same image, other command)
│  │  ├─ config.py          # settings from the environment (pydantic-settings)
│  │  ├─ llm.py             # LLMClient: chat, embed, transcribe (OpenAI)
│  │  ├─ core/              # database, jobs, audit, errors, events
│  │  └─ modules/
│  │     ├─ auth/           # profiles, PIN, sessions, roles
│  │     ├─ storage/        # save_file(), open_file()
│  │     ├─ knowledge/      # ingestion, chunking, search
│  │     ├─ assistant/      # safety level, translate, retrieve, answer, verify
│  │     ├─ fleet/          # karts, service events, repair notes, alerts
│  │     ├─ issues/         # reported problems with photos
│  │     ├─ inventory/      # parts, stock
│  │     ├─ supercube/      # GraphQL client, fake client
│  │     └─ tasks/          # to-dos, notifications
│  │        (each module: models.py, schemas.py, service.py, router.py, errors.py, README.md)
│  ├─ prompts/              # translate_v1.md, answer_v1.md
│  ├─ safety/               # emergency and HV word lists, Supercube's fixed texts
│  ├─ migrations/           # Alembic
│  ├─ tests/                # pytest, one folder per module
│  ├─ pyproject.toml
│  └─ Dockerfile
├─ frontend/                # React + TypeScript + Vite PWA
│  └─ src/
│     ├─ components/ui/     # buttons, cards, chips, MicButton, CameraCapture
│     ├─ features/          # login, karts, chat, issues, stock, todos
│     │                     # (each: api.ts, pages/, components/)
│     ├─ i18n/              # nl, fr, en, including error messages
│     ├─ lib/               # api client, error helper
│     └─ App.tsx            # routes
├─ web/                     # nginx config and Dockerfile for the web container
├─ eval/                    # questions.csv, run_eval.py, results/
├─ .github/workflows/       # ci.yml, release.yml
├─ compose.yaml             # db, api, worker, web
├─ compose.dev.yaml         # local overrides (hot reload, no TLS)
├─ .env.example             # names only, no values
├─ .pre-commit-config.yaml
└─ README.md
```

The module template and the steps to add a feature are in [Architecture](Architecture.md).

## Local setup (target: running in 15 minutes)

1. Install Git, Docker Desktop, Python 3.12, Node 20 LTS and VS Code.
2. Clone the repository, copy `.env.example` to `.env` and fill in the OpenAI key.
3. `docker compose -f compose.yaml -f compose.dev.yaml up -d db`
4. Backend: `cd backend`, create a virtual environment, `pip install -e .[dev]`, `alembic upgrade head`, `uvicorn app.main:app --reload`.
5. Worker: `python -m app.worker` in a second terminal.
6. Frontend: `cd frontend`, `npm install`, `npm run dev`.
7. `pre-commit install` once, so formatting runs before every commit.
8. Upload the handbook through the admin screen (the PDF is shared privately, outside git, through a channel agreed with Supercube; see [Open questions](../01%20Project/Open%20questions.md)).

Locally the app runs on `localhost`, which browsers treat as secure, so the camera and microphone work without a certificate.

## Environment variables

| Name | Example or note |
| --- | --- |
| `DATABASE_URL` | `postgresql+psycopg://mechai:…@db:5432/mechai` |
| `OPENAI_API_KEY` | Never in git |
| `CHAT_MODEL` / `EMBED_MODEL` / `STT_MODEL` | Model names; `EMBED_MODEL=text-embedding-3-small` |
| `FILES_DIR` | `/data/files` (the Docker volume) |
| `SUPERCUBE_CLIENT` | `fake` or `real` |
| `SUPERCUBE_API_URL` / `SUPERCUBE_TOKEN` | Only when access is granted |
| `AI_ENABLED` | `true` / `false` (retrieval-only mode) |
| `QUESTIONS_PER_HOUR` / `DAILY_QUESTION_CAP` | Cost guards |
| `AUTH_MODE` | `dev` (pick a user without a PIN, local only) or `pin` |

## Tooling and code quality

- **Python:** ruff (lint and format), mypy, pytest with coverage. Integration tests start a throwaway PostgreSQL container (testcontainers).
- **AI in tests:** a fake `LLMClient` returns fixed JSON, so unit tests are free and fast. Only the evaluation calls the real model.
- **Frontend:** ESLint, Prettier, Vitest; Playwright for one end-to-end flow (sign in, ask about kart 07, report an issue).
- **Pre-commit hooks:** ruff, Prettier, ESLint and a secret scanner (gitleaks). CI runs the same checks, so unformatted code cannot be merged.

## Way of working

- **GitHub flow:** a branch per task (`feat/hybrid-search`), a pull request, review by the other teammate, CI green, squash-merge to `main`.
- **Commits:** Conventional Commits (`feat:`, `fix:`, `docs:`, `test:`).
- **Versions:** `v0.1.0` (walking skeleton), `v0.5.0` (December prototype), `v1.0.0` (Showdown). `CHANGELOG.md` updated per release.
- **Definition of Done** (to confirm by the team): code reviewed, formatted and linted, tests added and green, error codes added, evaluation not worse, docs updated (module README or this vault), task closed in [To Do](../09%20To%20Do/To%20Do.md).
- **Prompts are code:** a prompt change is a new file version (`answer_v2.md`) and shows up in the evaluation results.
