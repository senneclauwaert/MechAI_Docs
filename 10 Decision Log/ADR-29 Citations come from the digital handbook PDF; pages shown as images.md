---
id: "ADR-29"
area: "AI"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-29 Citations come from the digital handbook PDF; pages shown as images

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** Supercube shared the handbook as a digital PDF with real text, where the PDF page equals the printed page.

**Decision:** Citations use the PDF's section and page numbers. Every page is rendered to an image at ingestion and shown in the chat (tap to zoom). Electrical questions show the wiring-diagram page (pages 81-89) as an image. The AI never writes wiring facts. Photos are needed only for Supercube's own AR parts that are not in the handbook.

**Why:** The mechanic always sees the original page; drawings and tables stay exact; no photographing needed.

**Alternatives considered:** Photographing every page (ADR-19); letting the AI describe diagrams.

**Consequences:** See [Handbook ingestion and parsing](../04%20RAG%20and%20AI/Handbook%20ingestion%20and%20parsing.md).
