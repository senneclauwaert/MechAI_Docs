---
id: "ADR-3"
area: "Hosting"
status: "Superseded by ADR-24"
date: "2026-10-10"
tags: [decision]
updated: 2026-11-06
---
# ADR-3 Azure managed services, not a VM

Back to [Decision Log](Decision%20Log.md)

**Status:** Superseded by ADR-24

**Context:** The project was going to run on Azure with the student credit.

**Decision:** Azure managed services (Container Apps, PostgreSQL Flexible Server, Blob Storage) instead of one virtual machine.

**Why:** No server to patch; scale to zero to save credit.

**Alternatives considered:** One virtual machine.

**Consequences:** Replaced on 6 November 2026: MechAi runs on Supercube's own server. See [ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md).
