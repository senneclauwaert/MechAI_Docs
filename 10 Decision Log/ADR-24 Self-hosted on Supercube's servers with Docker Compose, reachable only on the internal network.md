---
id: "ADR-24"
area: "Hosting"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** The plan was to host on Azure with the student credit. Running on Supercube's own servers keeps the data inside the company and costs nothing extra.

**Decision:** MechAi runs as Docker containers (`db`, `api`, `worker`, `web`) started with Docker Compose on Supercube's server. It is reachable only on Supercube's internal network, over HTTPS with a certificate from Supercube IT. Kubernetes files can be added if Supercube's IT uses Kubernetes.

**Why:** Company data stays on Supercube's hardware; no cloud bill; no student credit that runs out; simple to run with one command.

**Alternatives considered:** Azure managed services; one cloud virtual machine; Kubernetes from the start.

**Consequences:** Needs a server, an internal hostname and a certificate from Supercube IT. Images are built by GitHub Actions and pulled on the server. See [Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md).
