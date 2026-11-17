---
id: "ADR-31"
area: "Frontend"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-17
---
# ADR-31 Hands-free design: voice input, quick picks, big buttons

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** Mechanics work with dirty hands or gloves; nobody wants to type.

**Decision:** Voice input through Mistral speech-to-text (Voxtral, [ADR-38](ADR-38%20Mistral%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md)) wherever text is asked (part of the December demo); quick-pick buttons; a photo instead of words; touch targets of at least 56 px; at most three taps for the main tasks; a step-by-step mode with optional read-aloud in semester 2.

**Why:** A tool that needs typing will not be used in the workshop.

**Alternatives considered:** Typed input only; the browser's own speech recognition (not supported everywhere).

**Consequences:** See [Voice input and hands-free use](../05%20Features/Voice%20input%20and%20hands-free%20use.md).
