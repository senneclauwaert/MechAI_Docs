---
id: "ADR-9"
area: "AI"
status: "Accepted"
date: "2026-10-16"
tags: [decision]
updated: 2026-11-06
---
# ADR-9 Store answer traces in our own Postgres table

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · confirmed 6 Nov 2026

**Context:** Every answer must be traceable for debugging and for the evaluation chapter. Traces contain handbook text, which must stay private.

**Decision:** One row per question in `assistant.traces`: question, retrieved chunks and scores, prompt version, model, document revision, tokens, cost, latency, answer, verification flags, error code and feedback.

**Why:** Free, private (it stays on Supercube's server), queryable with SQL and directly usable for the evaluation.

**Alternatives considered:** Langfuse (self-hosted or cloud); an observability SaaS.

**Consequences:** Traces are kept for 90 days (proposed). No handbook text goes into plain logs.
