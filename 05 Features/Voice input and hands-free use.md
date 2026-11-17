---
id: "FEAT-15"
priority: "Must have"
area: "Frontend"
sprint: "Sprint 2"
december: "In (voice questions in the demo)"
tags: [feature]
updated: 2026-11-17
---
# Voice input and hands-free use

Back to [Features](Features.md)

## User story

As a mechanic with dirty hands or gloves, I speak instead of typing, tap big buttons and pick from quick choices, so I can use MechAi in the middle of a repair.

## What it includes

- A big microphone button wherever text is asked (assistant, issue description, repair log).
- Speech-to-text through the Mistral API (Voxtral); the text is shown so the user can check it before sending.
- Quick-pick buttons instead of free text where possible (reason for an issue, feedback reasons, common repairs).
- A photo instead of a description.
- Touch targets of at least 56 px; at most three taps for the main tasks.
- Step-by-step mode with big Next and Back buttons and optional read-aloud (semester 2).

## Planning

- **Sprint:** Sprint 2 (Must have).
- **December prototype:** In (voice questions in the demo).
- **Requirements:** FR-02, FR-12; US-04, US-22 (see [Requirements (functional & non-functional)](../02%20Analysis/Requirements%20%28functional%20&%20non-functional%29.md) and [MVP User Stories](../02%20Analysis/MVP%20User%20Stories.md)).

## Related

[ADR-31 Hands-free design- voice input, quick picks, big buttons](../10%20Decision%20Log/ADR-31%20Hands-free%20design-%20voice%20input,%20quick%20picks,%20big%20buttons.md), [Answer model (LLM)](../04%20RAG%20and%20AI/Answer%20model%20%28LLM%29.md)
