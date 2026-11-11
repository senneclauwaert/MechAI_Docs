---
id: "ADR-8"
area: "Frontend"
status: "Accepted"
date: "2026-10-16"
tags: [decision]
updated: 2026-11-06
---
# ADR-8 Frontend: React + TypeScript + Vite PWA, three.js for the 3D exploded view

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · confirmed 6 Nov 2026

**Context:** The frontend must be an installable web app on shared tablets and phones. On 6 November 2026 React with Vite, Next.js and Vue were compared.

**Decision:** React with TypeScript, built with Vite, as a PWA. three.js (react-three-fiber) for the 3D view in semester 2.

**Why:** A PWA is a static app served by the backend's nginx; Vite builds exactly that, with no server-side rendering needed. React has the largest ecosystem and the best three.js support. Next.js adds a server we don't need on an internal network; Vue would work but has a smaller ecosystem for our needs.

**Alternatives considered:** Next.js; Vue with Vite; a native app.

**Consequences:** The `web` container serves the built files. See [Architecture](../03%20Architecture/Architecture.md).
