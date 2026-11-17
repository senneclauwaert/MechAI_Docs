---
tags: [architecture, errors, quality]
updated: 2026-11-17
---
# Error handling

Back to [Architecture](Architecture.md) · Decision: [ADR-32 One error format with module error codes](../10%20Decision%20Log/ADR-32%20One%20error%20format%20with%20module%20error%20codes.md)

> [!IMPORTANT]
> Every error in MechAi has a **code**, a **message** and a **reference id**. Nothing fails silently. The mechanic sees a short, friendly message in their own language with the code; the team finds the full details in the logs with the reference id.

## The error shape

Every API error returns the right HTTP status and this body:

```json
{
  "error": {
    "code": "INVENTORY_STOCK_NEGATIVE",
    "message": "Not enough stock for this part.",
    "reference": "req_7f3a2c"
  }
}
```

- **code:** fixed, upper case, starts with the module prefix. The frontend uses it to pick the translated message.
- **message:** a short English description for developers and logs.
- **reference:** the request id. The same id is in every log line of that request.

## Module prefixes

| Module | Prefix | Examples |
| --- | --- | --- |
| core | `CORE_` | `CORE_VALIDATION_FAILED`, `CORE_NOT_FOUND`, `CORE_RATE_LIMITED`, `CORE_INTERNAL` |
| auth | `AUTH_` | `AUTH_PIN_WRONG`, `AUTH_PROFILE_LOCKED`, `AUTH_SESSION_EXPIRED`, `AUTH_FORBIDDEN` |
| storage | `STORAGE_` | `STORAGE_FILE_TOO_LARGE`, `STORAGE_TYPE_NOT_ALLOWED`, `STORAGE_FILE_MISSING` |
| knowledge | `KNOWLEDGE_` | `KNOWLEDGE_PARSE_FAILED`, `KNOWLEDGE_EMBEDDING_FAILED`, `KNOWLEDGE_PAGE_NOT_FOUND` |
| assistant | `ASSISTANT_` | `ASSISTANT_AI_UNAVAILABLE`, `ASSISTANT_AI_DISABLED`, `ASSISTANT_TRANSCRIBE_FAILED`, `ASSISTANT_DAILY_LIMIT` |
| fleet | `FLEET_` | `FLEET_KART_NOT_FOUND`, `FLEET_NOTE_NOT_EDITABLE` |
| issues | `ISSUES_` | `ISSUES_NOT_FOUND`, `ISSUES_TOO_MANY_PHOTOS` |
| inventory | `INVENTORY_` | `INVENTORY_STOCK_NEGATIVE`, `INVENTORY_PART_NOT_FOUND`, `INVENTORY_DUPLICATE_REQUEST` |
| supercube | `SUPERCUBE_` | `SUPERCUBE_UNREACHABLE`, `SUPERCUBE_REJECTED`, `SUPERCUBE_POD_UNKNOWN`, `SUPERCUBE_AUTH_FAILED`, `SUPERCUBE_KART_IN_REPAIR` |
| tasks | `TASKS_` | `TASKS_NOT_FOUND` |

The full list lives in code, in each module's `errors.py`, and is exported to a generated table in the code repository's docs. A test fails if two errors share a code.

## How it works in the backend

```python
# backend/app/core/errors.py
class AppError(Exception):
    status = 400
    def __init__(self, code: str, message: str, status: int | None = None):
        self.code, self.message = code, message
        if status:
            self.status = status

# backend/app/modules/inventory/errors.py
from app.core.errors import AppError

def stock_negative() -> AppError:
    return AppError("INVENTORY_STOCK_NEGATIVE", "Not enough stock for this part.", 409)
```

- A service raises an `AppError`; one FastAPI exception handler turns it into the error shape.
- Any other exception becomes `CORE_INTERNAL` (HTTP 500). The full stack trace goes to the log with the reference id, never to the screen.
- Validation errors from Pydantic become `CORE_VALIDATION_FAILED` with the field names.

## How it works in the frontend

- One `api.ts` helper reads the error body for every call.
- The message shown is looked up by code in the translation files (Dutch, French, English), for example `INVENTORY_STOCK_NEGATIVE` → "Niet genoeg voorraad voor dit onderdeel."
- Under the message, in small text: the code and the reference, so a mechanic can pass them on.
- Unknown codes fall back to a general message with the code.

## Background jobs and the worker

- A failed job stores the error code and message in `core.jobs.last_error` and is retried up to 3 times with a delay.
- The admin's upload screen shows the job status and the error code in plain words.

## Assistant fallbacks

| Problem | What the mechanic sees |
| --- | --- |
| Mistral API down or too slow | Retrieval-only mode: the relevant pages, plus "Steps unavailable, here are the pages" (`ASSISTANT_AI_UNAVAILABLE`) |
| AI answers switched off by an admin | The relevant pages (`ASSISTANT_AI_DISABLED`) |
| Speech-to-text failed | "Could not understand the recording, try again or type" (`ASSISTANT_TRANSCRIBE_FAILED`) |
| A number in the answer is not on the cited page | All generated steps are dropped; the pages are shown (retrieval-only mode); the trace is flagged |

## Rules

- Never swallow an error: log it or return it.
- Never show a stack trace, a SQL error or an AI provider error text to the user.
- Never put secrets or handbook text in an error message.
- Every new error gets a code in the module's `errors.py` and a translation in the frontend in the same pull request.
