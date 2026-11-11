---
id: "FEAT-10"
priority: "Must have"
area: "Platform"
sprint: "Sprint 1 (CI), sprint 3 (deployment)"
december: "In (CI from sprint 1; the demo runs on Docker Compose)"
tags: [feature]
updated: 2026-11-06
---
# Deployment and CI-CD

Back to [Features](Features.md)

## User story

As the team, we want every pull request checked automatically and every release deployable on Supercube's server with one command.

## What it includes

- Every pull request runs formatting and lint checks, type checks, tests, the retrieval evaluation and a Docker build.
- CI runs the retrieval evaluation on a small fake manual and fails if recall drops below its baseline. The real evaluation runs on the server, per handbook version.
- A merge to `main` builds the images and pushes them to the GitHub container registry.
- On the server: `docker compose pull && docker compose up -d`; migrations run at start; a smoke test calls the health endpoint.
- Secrets live in `.env` on the server, never in git.

## Planning

- **Sprint:** Sprint 1 (CI), sprint 3 (deployment) (Must have).
- **December prototype:** In (CI from sprint 1; the demo runs on Docker Compose).
- **Requirements:** NFR maintainability; US-24 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md), [Repo & dev setup](../03%20Architecture/Repo%20&%20dev%20setup.md), [ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](../10%20Decision%20Log/ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md)
