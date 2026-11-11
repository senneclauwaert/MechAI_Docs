---
id: "ADR-33"
area: "Process"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-33 Docs shared through a private GitHub repository; internal notes kept apart

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** Nehad, the teachers and people at Supercube need access to the documentation. The AI working notes should not be shared.

**Decision:** The Obsidian vault is a private GitHub repository, synced with the Obsidian Git plugin. Senne and Nehad can edit; teachers and Supercube are invited with read access. Links use standard Markdown so GitHub shows them. The folder `00 Internal` is in `.gitignore` and never shared. A PDF export is made on request. No public website.

**Why:** Version history, access control and a readable view on GitHub without extra tools.

**Alternatives considered:** A shared cloud drive; Obsidian Sync; a public documentation website.

**Consequences:** Internal notes reach Nehad only by other means. See [README](../README.md).
