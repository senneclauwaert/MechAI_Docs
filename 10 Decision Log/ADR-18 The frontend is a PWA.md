---
id: "ADR-18"
area: "Frontend"
status: "Accepted"
date: "2026-10-05"
tags: [decision]
updated: 2026-11-06
---
# ADR-18 The frontend is a PWA

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** Mechanics use shared tablets and their phones; a native app would mean two app stores.

**Decision:** MechAi is a progressive web app (PWA): a website that installs like an app and can use the camera and the microphone.

**Why:** One codebase for every device; no app store.

**Alternatives considered:** Native Android and iOS apps; a plain website.

**Consequences:** A PWA needs HTTPS, also on the internal network ([Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md)).
