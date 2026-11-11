---
id: "ADR-36"
area: "Architecture"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-36 Engineering safeguards: jobs, stock moves, document revisions, test set, Supercube checklist

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** The second outside review listed small technical risks.

**Decision:** (1) Safer jobs: `locked_until`, `attempts`, `last_error` and `run_after` on the jobs table. (2) Safe stock moves: one transaction with a request id; stock never below zero. (3) Document revisions: `revision`, `published_on`, `superseded_by`; ask Supercube whether rev 12 or V13 is current. (4) A richer test set with held-back questions. (5) One permissions checklist signed by Supercube.

**Why:** Each prevents a known failure (a stuck job, a double stock move, an answer from an old revision, overfitted tuning, missing permission).

**Alternatives considered:** Leaving them for later.

**Consequences:** See [Data model](../03%20Architecture/Data%20model.md), [Evaluation](../04%20RAG%20and%20AI/Evaluation.md) and [Questions for Supercube](../01%20Project/Questions%20for%20Supercube.md).
