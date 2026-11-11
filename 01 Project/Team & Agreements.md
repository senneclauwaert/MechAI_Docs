---
tags: [project, team]
updated: 2026-11-06
---
# Team & Agreements

Back to [Final Work Hub](../Final%20Work%20Hub.md)

## Team

| Name | Proposed role | Focus |
| --- | --- | --- |
| Senne Clauwaert | AI and backend lead, Supercube contact *(to confirm)* | Knowledge and assistant modules (handbook ingestion, RAG pipeline, prompts), the test set and evaluation, safety rules, the Supercube integration. Senne works at Supercube as a mechanic, so Senne owns the domain questions |
| Nehad | Frontend and platform lead *(to confirm)* | React PWA (chat with voice input, karts, stock, photo issues, 3D view), the fleet, issues and inventory modules, Docker Compose and CI/CD |

> [!IMPORTANT]
> The role split is still to confirm. The proposal gives each person one end-to-end area. Whatever we choose, both of us review each other's pull requests, so both can explain the whole system to the jury.

## Stakeholders

- **Client:** Supercube, contact person Ruben.
- **Senior mechanic** who approves repair notes and does the safety review: *to confirm*.
- **School coach:** *to confirm*.
- **Readers of this documentation:** the team, our teachers and the people at Supercube. Notes for the team only are kept apart and are not shared ([ADR-33 Docs shared through a private GitHub repository; internal notes kept apart](../10%20Decision%20Log/ADR-33%20Docs%20shared%20through%20a%20private%20GitHub%20repository;%20internal%20notes%20kept%20apart.md)).

## Team agreements (to confirm)

- **Communication:** *channel to confirm* (WhatsApp or Teams). Every decision ends up in the [Decision Log](../10%20Decision%20Log/Decision%20Log.md).
- **Weekly meeting:** 30 minutes at the start of each week: what is done, what is next, what blocks us. A sprint review and planning every second week.
- **Git workflow:** GitHub flow. One branch per task (`feat/…`, `fix/…`), then a pull request. The other person reviews within 24 hours, CI must be green, and we squash-merge to `main`. Nobody pushes to `main` directly.
- **Code quality:** all code is modular, easy to read, without duplication, cleanly formatted, and handles every error with a clear error code and description. Formatting and linting run automatically before every commit and in CI ([ADR-15 Simple, readable code with one copy-paste module template](../10%20Decision%20Log/ADR-15%20Simple,%20readable%20code%20with%20one%20copy-paste%20module%20template.md), [ADR-32 One error format with module error codes](../10%20Decision%20Log/ADR-32%20One%20error%20format%20with%20module%20error%20codes.md)).
- **Definition of Done:** reviewed by the other person, tests added and green, evaluation not worse, errors handled with error codes, documentation updated, and the task marked done in [To Do](../09%20To%20Do/To%20Do.md).
- **Documentation:** this vault is the single source of documentation. It lives in a private GitHub repository that both of us sync with the Obsidian Git plugin.
- **When someone misses a deadline:** say so as soon as you know. We re-plan together at the next weekly meeting, and we cut scope before we cut quality.
