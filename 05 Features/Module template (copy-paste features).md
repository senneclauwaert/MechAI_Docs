---
id: "FEAT-13"
priority: "Must have"
area: "Platform"
sprint: "Sprint 1"
december: "In"
tags: [feature]
updated: 2026-11-06
---
# Module template (copy-paste features)

Back to [Features](Features.md)

## User story

As the team, we want every feature built from the same simple module layout, so adding a feature is copy, rename and change.

## What it includes

- Backend modules all have `models.py`, `schemas.py`, `service.py`, `router.py`, `errors.py` and a README.
- Frontend features all have `api.ts`, `pages/` and `components/`.
- Shared code lives only in `core/` and `components/ui/`.
- Formatting and linting are automatic (ruff, Prettier, ESLint) through pre-commit and CI.
- A reviewer can follow any endpoint from router to service to model in a minute.

## Planning

- **Sprint:** Sprint 1 (Must have).
- **December prototype:** In.
- **Requirements:** NFR maintainability; US-25 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[Architecture](../03%20Architecture/Architecture.md), [ADR-15 Simple, readable code with one copy-paste module template](../10%20Decision%20Log/ADR-15%20Simple,%20readable%20code%20with%20one%20copy-paste%20module%20template.md)
