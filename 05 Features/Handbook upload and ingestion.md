---
id: "FEAT-6"
priority: "Must have"
area: "Knowledge"
sprint: "Sprint 1"
december: "In (the whole handbook once Supercube gives its written OK; test pages until then)"
tags: [feature]
updated: 2026-11-06
---
# Handbook upload and ingestion

Back to [Features](Features.md)

## User story

As an admin, I upload the handbook PDF, and it becomes searchable with its section and page numbers kept.

## What it includes

- Upload a PDF through the admin screen; the worker on Supercube's server processes it.
- Docling reads the text (no OCR needed); the text is split into sections and chunks with section number, heading and page range.
- Every page is rendered as an image for the chat.
- Only new or changed chunks are embedded (content hash).
- Each upload is a document revision; a new revision becomes current only after the evaluation passes.
- The job status and any error code are visible (waiting, running, done, failed).
- The handbook never goes into git.

## Planning

- **Sprint:** Sprint 1 (Must have).
- **December prototype:** In (the whole handbook once Supercube gives its written OK; test pages until then).
- **Requirements:** FR-20 to FR-22; US-03 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[Handbook ingestion and parsing](../04%20RAG%20and%20AI/Handbook%20ingestion%20and%20parsing.md), [RAG pipeline (build spec)](../03%20Architecture/RAG%20pipeline%20%28build%20spec%29.md)
