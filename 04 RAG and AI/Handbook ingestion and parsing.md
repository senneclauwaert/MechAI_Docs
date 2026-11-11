---
tags: [rag, data, handbook]
updated: 2026-11-06
---
# Handbook ingestion and parsing

Back to [RAG and AI](RAG%20and%20AI.md) · Decisions: [ADR-17 Docling for parsing and OCR](../10%20Decision%20Log/ADR-17%20Docling%20for%20parsing%20and%20OCR.md), [ADR-29 Citations come from the digital handbook PDF; pages shown as images](../10%20Decision%20Log/ADR-29%20Citations%20come%20from%20the%20digital%20handbook%20PDF;%20pages%20shown%20as%20images.md)

**Parsing** means turning a PDF into clean text with its structure: headings, tables and page numbers. Getting the handbook in well is the foundation of the whole assistant. The exact steps are in [RAG pipeline (build spec)](../03%20Architecture/RAG%20pipeline%20%28build%20spec%29.md).

## The handbook

Supercube shared the handbook as a PDF on 6 November 2026:

- **"KART STORM – User and Maintenance Handbook"** by OTL Italia, 89 pages, A4, English.
- File name `STORM_HANDBOOK_V13_ENG_01082017.pdf`; the page footer says "rev 12 IT 01-08-2017". Which revision is current is asked in [Questions for Supercube](../01%20Project/Questions%20for%20Supercube.md).
- The file is kept privately and **never goes into git** or any public place.

What we checked:

- **It is a digital PDF, not a scan.** Almost every page has selectable text, so **no OCR is needed**.
- **The PDF page number equals the printed page number**, so the citation "page 17" is simply the PDF page.
- **Clear numbered sections** (for example 4.5.16 Rear axle and bearings, 5.3 Rear mechanical section, 6.2.1 Failure codes). These become our sections.
- **One language: English.** Questions in Dutch or French are translated into English search terms first.

Points to watch:

- **The failure code table (pages 55-56)** loses its code numbers in plain text extraction. If Docling also misses them, the short table is entered by hand once and checked by a senior mechanic.
- **The wiring diagrams (pages 81-89)** are drawings. They are shown as images, never interpreted by the AI (see below). The symbol table on page 85 is real text and is indexed.
- **The handbook covers the base OTL Storm kart**, including versions Supercube may not use. Supercube's own AR parts (headset, the PC in the steering wheel, the network switch) are **not in the handbook**. Questions about them get "not in the handbook" until approved repair notes or Supercube documents cover them.
- **Real pages for the demo:** 4.5.16 Rear axle and bearings (page 17), 5.3 Rear mechanical section (pages 38-42), 5.6.2 Replacing the drive shaft bearings (page 48).

## The parser: Docling

Docling is free (MIT licence) and handles reading order, tables and page numbers in one tool. OCR is switched off because the PDF has real text, which keeps it light enough to run in the worker on Supercube's server.

Compared with: Unstructured (many system dependencies), PyMuPDF (AGPL licence, risky if Supercube keeps the software), Marker and MinerU (licence conditions; MinerU prefers a GPU). PyMuPDF's licence is also why page rendering uses `pypdfium2` (Apache/BSD) instead. **To confirm** when building.

## Where ingestion runs

In the **worker on Supercube's server**, when an admin uploads a PDF through the admin screen. No separate script on a laptop is needed. A new revision is processed the same way, and only changed chunks get new embeddings ([Embeddings and reranker](Embeddings%20and%20reranker.md)).

## Page images in the chat

Every page is rendered to a PNG at ingestion and stored on the `files` volume. When the assistant cites a page, the page image is shown under the answer; tapping it opens it full screen with zoom. This lets the mechanic check the source and see drawings and tables exactly as printed.

## Wiring diagrams

Text extraction on a diagram gives scattered labels without connections: useless, and even dangerous. So:

1. Diagram pages (81-89) are marked as diagrams.
2. Their captions, titles and nearby text are searchable, so "wiring diagram of the controller" finds the right page.
3. For electrical questions the matching diagram page is shown as an image in the chat. The mechanic reads the diagram.
4. **The AI never states a wire colour or a pin number on its own.** If exact pin tables are needed, they are entered by hand once, checked by a senior mechanic, and read as plain data.

## Photos

Photographing pages is no longer needed: the PDF has every page. Photos are only needed for Supercube's own AR parts that are not in the handbook, if documentation for them is missing.

## Copyright and permission

The handbook belongs to OTL Italia. Having the PDF is not the same as permission: Supercube's written OK is needed to use it in MechAi and to send short excerpts to the OpenAI API. Only a few example pages are shown at school.
