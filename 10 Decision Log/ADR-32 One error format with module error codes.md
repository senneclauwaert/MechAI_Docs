---
id: "ADR-32"
area: "Architecture"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-32 One error format with module error codes

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** Errors must be handled everywhere, with clear error codes and descriptions, so problems can be found and explained quickly.

**Decision:** Every error is `{code, message, reference}`. Each module has an `errors.py` with its own prefix (`AUTH_`, `FLEET_`, `INVENTORY_`, `ASSISTANT_`, `SUPERCUBE_`, …). The interface shows a friendly message in the user's language with the code. Unknown exceptions become `CORE_INTERNAL` and are logged with the reference.

**Why:** Users can report a problem precisely; the team finds the log line in seconds; nothing fails silently.

**Alternatives considered:** Free-form error messages; HTTP status codes only.

**Consequences:** See [Error handling](../03%20Architecture/Error%20handling.md).
