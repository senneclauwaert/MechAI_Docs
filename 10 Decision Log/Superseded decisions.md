---
tags: [decision, history]
updated: 2026-11-06
---
# Superseded decisions

Back to [Decision Log](Decision%20Log.md)

The plan changed a lot in October 2026. This note lists every earlier choice or recommendation that a later decision replaced, newest first. We keep them on purpose: the analysis should explain why the plan changed, and the jury may ask why we did not use, for example, a local model or microservices.

| Replaced on | What we planned before | What replaced it | Why |
| --- | --- | --- | --- |
| 6 Nov 2026 | **Azure hosting** (Container Apps, PostgreSQL Flexible Server, Blob Storage, Key Vault, Bicep) with the student credit | **Docker Compose on Supercube's own server**, internal network only ([ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md)) | Company data stays on Supercube's hardware; no cloud bill or credit limit |
| 6 Nov 2026 | **Azure OpenAI** for answers and embeddings | **The OpenAI API** directly, also for speech-to-text ([ADR-25 OpenAI API for answers, embeddings and speech-to-text](ADR-25%20OpenAI%20API%20for%20answers,%20embeddings%20and%20speech-to-text.md)) | No Azure any more; one provider for all three jobs |
| 6 Nov 2026 | Four retrieval steps built at once | Baseline first, one step at a time ([ADR-27 Baseline-first retrieval with English query translation](ADR-27%20Baseline-first%20retrieval%20with%20English%20query%20translation.md)) | Advice of both reviews; clearer measurements |
| 6 Nov 2026 | Photographing the handbook pages, named by page number | The digital PDF; pages rendered as images ([ADR-29 Citations come from the digital handbook PDF; pages shown as images](ADR-29%20Citations%20come%20from%20the%20digital%20handbook%20PDF;%20pages%20shown%20as%20images.md)) | Supercube shared the PDF |
| 6 Nov 2026 | Ingestion on a laptop, with OCR | Ingestion in the worker on the server, without OCR | The PDF has real text |
| 6 Nov 2026 | AI-written steps unlocked after four safety checkboxes | Three safety levels in code ([ADR-30 Safety levels enforced in code](ADR-30%20Safety%20levels%20enforced%20in%20code.md)) | The AI must not write safety plans |
| 6 Nov 2026 | Three roles (mechanic, senior, admin) | Four roles, with the operator ([ADR-26 Four roles- operator, mechanic, senior mechanic, admin](ADR-26%20Four%20roles-%20operator,%20mechanic,%20senior%20mechanic,%20admin.md)) | The operator notices problems first |
| 6 Nov 2026 | Read-only Supercube integration; never start diagnostics from MechAi | Status changes and diagnostics like the operator app ([ADR-23 Keep REST for our own API, talk to Supercube's GraphQL API through one adapter module](ADR-23%20Keep%20REST%20for%20our%20own%20API,%20talk%20to%20Supercube's%20GraphQL%20API%20through%20one%20adapter%20module.md)) | Same flow as Supercube's own app; every action logged |
| 6 Nov 2026 | Proposed device setup code per tablet | Not needed: internal network only | MechAi has no public URL |
| 6 Nov 2026 | Voice input "only if time allows" | Voice input in the December demo ([ADR-31 Hands-free design- voice input, quick picks, big buttons](ADR-31%20Hands-free%20design-%20voice%20input,%20quick%20picks,%20big%20buttons.md)) | Mechanics have dirty hands |
| 6 Nov 2026 | Two venues (Brussels and Gent) | One venue, Brussels, with a venue field for later | Current scope |
| 6 Nov 2026 | The 28 October UI design as the reference | The HTML prototype ([ADR-34 The HTML prototype is the official design; diagrams as Mermaid in the vault](ADR-34%20The%20HTML%20prototype%20is%20the%20official%20design;%20diagrams%20as%20Mermaid%20in%20the%20vault.md)); the 28 October UI was deleted | Senne preferred the HTML prototype |
| 6 Nov 2026 | Diagrams in FigJam | Mermaid diagrams in this vault ([Diagrams](../06%20Design%20and%20Prototypes/Diagrams.md)) | Stay in sync with the text; visible on GitHub |
| 6 Nov 2026 | Four sprints from 19 October to 13 December, jury around April 2027 | The school's day-track timeline, sprints from 9 November ([Planning & Deadlines](../01%20Project/Planning%20&%20Deadlines.md)) | The official timeline was published |
| 6 Nov 2026 | The LangChain starter as a prototype | Archived; plain Python for the build ([ADR-6 Plain Python + OpenAI SDK for the full build (LangChain only in the starter)](ADR-6%20Plain%20Python%20+%20OpenAI%20SDK%20for%20the%20full%20build%20%28LangChain%20only%20in%20the%20starter%29.md)) | Explainability |
| 24 Oct 2026 | Project docs in Notion | This Obsidian vault ([ADR-16 Project docs moved from Notion to the Obsidian vault MechAi](ADR-16%20Project%20docs%20moved%20from%20Notion%20to%20the%20Obsidian%20vault%20MechAi.md)) | The Notion free plan ran out of blocks |
| 24 Oct 2026 | Cloudflare Access in front of the app, like Supercube's operator app | No outside login for now; auth in one module ([ADR-12 No accounts- profile picker + personal PIN, 30-minute idle logout](ADR-12%20No%20accounts-%20profile%20picker%20+%20personal%20PIN,%2030-minute%20idle%20logout.md)) | Build standalone; Supercube may integrate it later. An outside login is not needed on the internal network |
| 24 Oct 2026 | QR or barcode scanning of parts and karts (in the plan since 5 October) | Pick from a list or search ([ADR-13 No QR codes](ADR-13%20No%20QR%20codes.md)) | Less to build and label; enough for identical karts |
| 16 Oct 2026 | Login with Microsoft Entra External ID (an identity provider) | Profile picker and personal PIN on shared tablets | Faster with gloves, no email accounts needed |
| 16 Oct 2026 | OpenTelemetry with a self-hosted Langfuse for answer traces | Traces in our own Postgres table ([ADR-9 Store answer traces in our own Postgres table](ADR-9%20Store%20answer%20traces%20in%20our%20own%20Postgres%20table.md)) | Free, private and usable for the evaluation chapter |
| 16 Oct 2026 | A separate "AI Context" page in Notion | A separate context file for AI assistants, kept outside the shared documentation | Senne did not want AI-only pages in the docs |
| 16 Oct 2026 | Demo case: fault E-21 after charging on kart 07 | A broken rear axle bearing on kart 07 | Senne's request; closer to a real repair |
| 16 Oct 2026 | The first FigJam board (8 diagrams, with Ollama and guessed dates) | Ten redrawn diagrams matching the architecture | The old board was out of date |
| 10 Oct 2026 | **Claude Haiku 4.5** through the Anthropic API as the answer model | **Azure OpenAI** ([ADR-2 Azure OpenAI for the answer model and embeddings](ADR-2%20Azure%20OpenAI%20for%20the%20answer%20model%20and%20embeddings.md)) | One provider, one bill, one EU region, managed identity |
| 10 Oct 2026 | **BGE-M3** embeddings run locally through Hugging Face | Azure OpenAI `text-embedding-3-small` | Everything in Azure; BGE-M3 may still be a comparison. See [Embeddings and reranker](../04%20RAG%20and%20AI/Embeddings%20and%20reranker.md) |
| 10 Oct 2026 | Phase 3 running until June 2027, jury guessed for 18 June 2027 | Phase 3 in February and March, jury around April 2027 | Senne confirmed the timeline |
| 10 Oct 2026 | Deciding later whether to switch to Claude Haiku 5.5 (ten times cheaper than Haiku 4.5) | Not relevant any more | The answer model became Azure OpenAI |
| 6 Oct 2026 | A local model through **Ollama** on the GPU desktop for development (Qwen3.5 9B or Gemma 4 12B) | No Ollama; first Claude Haiku 4.5, then Azure OpenAI | Needs our PC to be on, GPU memory unknown, hard to host for a demo |
| 6 Oct 2026 | A small Azure OpenAI model for the demo only (first research) | Claude Haiku 4.5 on 6 October; Azure OpenAI came back for everything on 10 October | Senne first chose the cheapest Claude model |
| 6 Oct 2026 | BGE-M3 through Ollama | BGE-M3 through Hugging Face (then replaced on 10 October) | No Ollama |
| 6 Oct 2026 | **Seven microservices** with an event bus and an API gateway, then **three services** | One modular backend plus one worker ([ADR-1 Modular monolith- one backend + one worker + one PostgreSQL, no microservices](ADR-1%20Modular%20monolith-%20one%20backend%20+%20one%20worker%20+%20one%20PostgreSQL,%20no%20microservices.md)) | Not required for the grade; too much work and cost for two people |
| 6 Oct 2026 | Plain Python only, no LangChain at all | The starter in LangChain; plain Python proposed for the full build | Senne asked for a LangChain starter. See [Framework choice](../04%20RAG%20and%20AI/Framework%20choice.md) |
| 5 Oct 2026 | A local Qwen3.5 model to describe wiring diagrams | A vision-capable Azure OpenAI GPT model | No local models |
| 5 Oct 2026 | Optimization baseline with BGE-M3, vector search and the top 8 chunks | Baseline with `text-embedding-3-small` and whole sections | Model change; parent-document lookup |

## What stays from the early research

Not everything from the early research was replaced. The modular monolith, Docling, PostgreSQL with pgvector and hybrid search with RRF, the PWA, the context headers in chunks, the test-set-first rule and the senior approval of repair notes all still stand. The original research report is linked in [Sources](../11%20Reference/Sources.md).
