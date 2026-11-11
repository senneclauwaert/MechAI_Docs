---
id: "ADR-17"
area: "AI"
status: "Accepted"
date: "2026-10-05"
tags: [decision]
updated: 2026-11-06
---
# ADR-17 Docling for parsing

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted · amended 6 Nov 2026

**Context:** The handbook must be turned into text with its structure and page numbers.

**Decision:** Docling parses the handbook. Since the handbook is a digital PDF (6 November 2026), OCR is switched off and ingestion runs in the worker on Supercube's server.

**Why:** Free (MIT licence); handles reading order, tables and page numbers in one tool.

**Alternatives considered:** Unstructured; PyMuPDF (AGPL licence); Marker; MinerU.

**Consequences:** No laptop ingestion script is needed. See [Handbook ingestion and parsing](../04%20RAG%20and%20AI/Handbook%20ingestion%20and%20parsing.md).
