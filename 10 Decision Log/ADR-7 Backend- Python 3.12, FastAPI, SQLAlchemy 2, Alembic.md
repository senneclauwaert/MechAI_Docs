---
id: "ADR-7"
area: "Architecture"
status: "Accepted"
date: "2026-10-16"
tags: [decision]
updated: 2026-11-17
---
# ADR-7 Backend: Python 3.12, FastAPI, SQLAlchemy 2, Alembic

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · confirmed 6 Nov 2026

**Context:** The backend needs a language and framework that fit the AI work and that both students can learn quickly.

**Decision:** Python 3.12 with FastAPI, SQLAlchemy 2 and Alembic for migrations. Confirmed by Senne on 6 November 2026.

**Why:** Python has the best AI and PDF libraries (the Mistral SDK, Docling). FastAPI gives validation, OpenAPI docs and good speed with little code.

**Alternatives considered:** Node.js with Express or NestJS; .NET; Django.

**Consequences:** Pydantic schemas per endpoint; the frontend generates its TypeScript client from the OpenAPI description.
