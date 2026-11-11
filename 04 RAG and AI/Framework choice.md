---
tags: [rag, code]
updated: 2026-11-06
---
# Framework choice

Back to [RAG and AI](RAG%20and%20AI.md) · Decision: [ADR-6 Plain Python + OpenAI SDK for the full build (LangChain only in the starter)](../10%20Decision%20Log/ADR-6%20Plain%20Python%20+%20OpenAI%20SDK%20for%20the%20full%20build%20%28LangChain%20only%20in%20the%20starter%29.md)

A **framework** such as LangChain gives ready-made building blocks: loaders, text splitters, retrievers and chains. It saves typing, but it hides what happens inside, and the jury will ask exactly what happens inside.

## Decision (6 November 2026)

**Plain Python with the official OpenAI SDK, behind our own small `LLMClient` class.** At most `langchain-text-splitters` may be used for splitting text.

**Why:**

- The grade depends on explaining every step. The pipeline has a handful of steps (safety level, translate, search, merge, answer, verify), and plain Python makes each step a function you can point at.
- Debugging is easier: our own functions and normal error messages with our own error codes.
- No lock-in to one library.

## Kept open

**LangChain and LangGraph stay open as options** (Senne, 6 November 2026). LangGraph is a library for building step-by-step flows with branches and loops. If the pipeline grows (for example a retry loop or routing questions to SQL), the team may revisit this. The plain-Python steps are written as separate functions, so they could be wrapped later.

## History

- 5 October 2026: the research advised plain Python only.
- 6 October 2026: a minimal LangChain starter was made at Senne's request, to see the parts quickly. It used Claude, BGE-M3 and Chroma and is now archived; updating it is no longer planned.
- 16 October 2026: plain Python proposed for the full build; confirmed on 6 November 2026.
