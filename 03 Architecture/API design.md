---
tags: [architecture, api]
updated: 2026-11-06
---
# API design

Back to [Architecture](Architecture.md)

> [!NOTE]
> REST and JSON under `/api/v1`. FastAPI generates the OpenAPI description at `/docs`; the frontend generates its TypeScript client from it. Each module's endpoints live in its own `router.py`. Supercube's GraphQL API is never called from the app directly, only through the `supercube` module ([Supercube integration (GraphQL)](Supercube%20integration%20%28GraphQL%29.md)).

**Roles:** **O** = operator, **M** = mechanic, **S** = senior mechanic, **A** = admin. "M+" means mechanic, senior and admin.

## Endpoints (first version)

| Method and path | What it does | Roles | Sprint |
| --- | --- | --- | --- |
| `GET /health` | Liveness and database check | public | 1 |
| `GET /auth/profiles` | Active profiles for the picker (name, photo, role) | public (internal network) | 1 |
| `POST /auth/pin-login` | Body: user_id, pin. Sets the session cookie. Rate limited per device; 5 wrong tries lock the profile for 5 minutes (not until an admin acts), so nobody can lock everyone out | public, rate limited | 1 |
| `POST /auth/logout` · `GET /auth/me` | Switch user; current profile and role | all | 1 |
| `POST /assistant/transcribe` | Audio in, text out (speech-to-text) | O, M+ | 2 |
| `POST /assistant/ask` | Body: kart_id, question, input (`typed`/`voice`), conversation_id?. Returns the safety level, the checked answer, sources with page images, trace_id | M+ | 1 |
| `POST /assistant/messages/{id}/feedback` | Thumbs up or down with a reason | M+ | 3 |
| `POST /assistant/messages/{id}/confirm-safety` | Logs the high-voltage confirmation | M+ | 2 |
| `GET /assistant/conversations?kart_id=` | Recent chats, optionally per kart | M+ | 3 |
| `POST /knowledge/documents` | Upload a handbook PDF; queues ingestion | A | 1 |
| `GET /knowledge/documents/{id}/status` | Ingestion progress and errors | A | 1 |
| `GET /knowledge/pages/{id}/image` | The rendered page image (served by the API) | M+ | 2 |
| `GET /knowledge/search?q=` | Search only, no AI (debugging and retrieval-only mode) | M+ | 1 |
| `GET /fleet/karts` · `GET /fleet/karts/{id}` | Kart list with status and open issues; one kart with history | all | 2 |
| `POST /fleet/karts/{id}/mark-broken` | Marks the kart broken in MechAi and in Supercube's system | O, M+ | 2 |
| `POST /fleet/karts/{id}/mark-repaired` | Marks the kart repaired in MechAi and in Supercube's system | M+ | 2 |
| `POST /fleet/karts/{id}/diagnostics` | Body: speed_mode (`PODLANE` / `CRUISE` / `BOOST` / `HIGH_BOOST` / `HIGH_BRAKE`), confirmed_clear (must be true). Starts diagnostics; refused with `SUPERCUBE_KART_IN_REPAIR` while someone else has an open repair; stops by itself after 60 s without a command | all | 3 |
| `DELETE /fleet/karts/{id}/diagnostics` | Stops diagnostics | all | 3 |
| `GET /fleet/karts/{id}/alerts?from=&to=` | Machine alerts of one kart (from Supercube) | M+ | Semester 2 (fake data earlier) |
| `POST /fleet/karts/{id}/service-events` · `PATCH /fleet/service-events/{id}` | Start or finish a repair | M+ | 3 |
| `POST /fleet/repair-notes` · `POST /fleet/repair-notes/{id}/submit` | Write a note; send it for review | M+ | Semester 2 |
| `POST /fleet/repair-notes/{id}/approve` · `/reject` | Senior review (PIN re-entered) | S | Semester 2 |
| `POST /issues` | Report an issue: kart_id, reason, description, severity, photos (multipart) | O, M+ | 2 |
| `GET /issues?kart_id=&status=` · `GET /issues/{id}` | Issues per kart or all open issues; one issue with photos | all | 2 |
| `PATCH /issues/{id}` | Change status; close with an optional "after" photo | M+ | 3 |
| `POST /issues/{id}/todo` | Turn the issue into a to-do | M+ | 3 (stretch) |
| `GET /files/{id}` | A stored photo, after a role check | all | 2 |
| `GET /inventory/parts?q=&low=true` | Search parts; low-stock filter | M+ | 3 |
| `POST /inventory/parts/{id}/take` | Take a part; header `Idempotency-Key` (request id) | M+ | 3 |
| `POST /inventory/parts` · `PATCH /inventory/parts/{id}` | Manage parts, restock, correct counts | A | 3 |
| `POST /admin/users` · `POST /admin/users/{id}/reset-pin` | Add profiles; unlock and reset a PIN | A | 1 |
| `POST /admin/ai-switch` | Turn AI answers on or off (retrieval-only mode) | A | 3 |
| `GET /tasks/todos` · `GET /tasks/notifications` | To-dos and notifications | M+ | Semester 2 |

## Conventions

- One request schema and one response schema per endpoint (Pydantic).
- **Errors** always use one shape, with the right HTTP status. See [Error handling](Error%20handling.md).

  ```json
  {"error": {"code": "INVENTORY_STOCK_NEGATIVE", "message": "Not enough stock for this part.", "reference": "req_7f3a2c"}}
  ```

- Lists are paginated with `?limit=&cursor=`.
- Times are UTC in ISO 8601; the frontend shows Brussels time.
- `POST /assistant/ask` is rate limited per user (start: 30 questions per hour, to be tuned). `POST /auth/pin-login` is rate limited per profile and per device.
- Uploads: images only (JPEG, PNG, WebP), at most 10 MB per photo and 6 photos per issue; audio at most 60 seconds.
- Every response carries a request id (`X-Request-Id`); answers also carry the trace id for feedback and debugging.
