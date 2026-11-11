---
tags: [reference, sources]
updated: 2026-11-06
---
# Sources

Back to [Final Work Hub](../Final%20Work%20Hub.md)

> [!NOTE]
> This list records the sources used while the plan was made, with the date each page was opened. Some sections describe options that were later replaced (for example Azure, local models or Claude prices); they are kept so every claim in the analysis can be traced. The current decisions are in the [Decision Log](../10%20Decision%20Log/Decision%20Log.md).

This note lists the sources behind the research, so the analysis can cite them. "Accessed" means the page had no date when it was opened. Prices and limits change, so re-check them before quoting them to the jury.

## 1. The RAG stack research (pages opened on 5 or 6 October 2026)

The full report is [Supercube RAG Platform: Research Report](https://claude.ai/code/artifact/356761ee-1c2a-4b50-9b12-7afe28d407c8). Its model choices (Ollama, BGE-M3) are outdated; see [Superseded decisions](../10%20Decision%20Log/Superseded%20decisions.md).

| Source | Date | Used for |
|---|---|---|
| [Azure for Students](https://azure.microsoft.com/en-us/free/students) | accessed | $100 credit, 12 months, no card; free Container Apps grant, PostgreSQL B1MS 750 h, Azure DevOps |
| [Microsoft Q&A: Azure for Students and Azure OpenAI](https://learn.microsoft.com/en-us/answers/questions/5699314/how-to-activate-azure-for-students-and-create-a-fr) | Jan to Feb 2026 | Students can deploy Azure OpenAI from credit; some regions limited |
| [Microsoft Foundry data privacy](https://learn.microsoft.com/en-us/azure/foundry/responsible-ai/openai/data-privacy) | 19 May 2026 | Prompts not used for training; data geography |
| [Azure OpenAI pricing](https://azure.microsoft.com/en-us/pricing/details/azure-openai/) | accessed | Model families listed; prices did not render, so not used for numbers |
| [pricepertoken.com](https://pricepertoken.com/endpoints/azure), Azure (secondary) | 4 Oct 2026 | GPT-5 nano and GPT-4.1 nano prices on Azure |
| [OpenAI API pricing](https://openai.com/api/pricing/) | accessed | GPT-5.6 Luna price, used as reference |
| [GitHub Docs: GitHub Models](https://docs.github.com/en/github-models/about-github-models) | accessed | Retired on 30 July 2026 |
| [Gemini API terms](https://ai.google.dev/gemini-api/terms) | 28 Apr 2026 | Free-tier data use; EEA users get paid-tier rules |
| [Gemini API pricing](https://ai.google.dev/gemini-api/docs/pricing) | accessed | Flash-Lite prices; which models have a free tier |
| [Gemini rate limits](https://ai.google.dev/gemini-api/docs/rate-limits) | accessed | Free-tier limits only visible in AI Studio |
| [Mistral: training opt-out](https://help.mistral.ai/en/articles/455207-can-i-opt-out-of-my-input-or-output-data-being-used-for-training) | 3 Sep 2026 | Training on API data by default; opt-out toggle |
| [Mistral pricing](https://mistral.ai/pricing) | accessed | Mistral Large price |
| [Groq data retention summary (secondary](https://humla.team/blog/groq-data-retention-policy), quotes Groq's agreement of 22 Jun 2026) | accessed | No training on inputs; data stored in the US |
| [Ollama: qwen3.5](https://ollama.com/library/qwen3.5), [gemma4](https://ollama.com/library/gemma4), [qwen3-embedding](https://ollama.com/library/qwen3-embedding) | accessed | Model sizes, file sizes, languages, modalities |
| [Google: Gemma 4 under Apache 2.0](https://opensource.googleblog.com/2026/03/gemma-4-expanding-the-gemmaverse-with-apache-20.html) | 2 Apr 2026 | Gemma 4 licence |
| [EuroEval](https://euroeval.com/) | accessed | Dutch and French LLM leaderboards exist; could not render them |
| [MTEB-NL and E5-NL (arXiv 2509.12340)](https://arxiv.org/html/2509.12340v1) | 15 Sep 2025 | Dutch retrieval scores of embedding models |
| [Qwen3-Embedding-0.6B card](https://huggingface.co/Qwen/Qwen3-Embedding-0.6B) | accessed | Licence, size, multilingual MTEB scores (vendor table) |
| [BGE-M3 card](https://huggingface.co/BAAI/bge-m3) | accessed | Licence, 8,192 tokens, dense, sparse and multi-vector output |
| [multilingual-e5-large-instruct card](https://huggingface.co/intfloat/multilingual-e5-large-instruct) | accessed | Licence, 512-token limit, query instruction |
| [lelabdev embedding benchmark (secondary)](https://github.com/lelabdev/embedding-benchmark) | 30 Jun 2026 | Only French comparison found; 4 queries, not significant |
| [Qwen3-Reranker-0.6B card](https://huggingface.co/Qwen/Qwen3-Reranker-0.6B) | accessed | Licence and vendor-reported reranker scores |
| [bge-reranker-v2-m3 card](https://huggingface.co/BAAI/bge-reranker-v2-m3) | accessed | Licence and size |
| [jina-reranker-v2-base-multilingual card](https://huggingface.co/jinaai/jina-reranker-v2-base-multilingual) | accessed | Non-commercial licence |
| [Docling GitHub](https://github.com/docling-project/docling), [Docling PyPI](https://pypi.org/project/docling/) | 3 Oct 2026 (v2.133.0) | Licence, features, OCR, VLM pipeline |
| [Unstructured GitHub](https://github.com/Unstructured-IO/unstructured) | accessed | Licence, system dependencies, open-source vs paid |
| [PyMuPDF docs](https://pymupdf.readthedocs.io/en/latest/about.html) | 3 Sep 2026 (v1.28.2) | AGPL or commercial licence |
| [Marker GitHub](https://github.com/datalab-to/marker) | accessed | Code and weights licences |
| [MinerU GitHub](https://github.com/opendatalab/MinerU) | accessed | Licence, version 4.0, hardware |
| [pgvector GitHub](https://github.com/pgvector/pgvector) | accessed (v0.8.7) | Index types, iterative scans, hybrid search, dimension limits |
| [pgvector on Azure PostgreSQL](https://learn.microsoft.com/en-us/azure/postgresql/extensions/how-to-use-pgvector) | 10 Jul 2026 | Enabling the vector extension on Azure |
| [Qdrant GitHub](https://github.com/qdrant/qdrant) | accessed | Licence, hybrid search, filtering |
| [Azure AI Search: hybrid ranking](https://learn.microsoft.com/en-us/azure/search/hybrid-search-ranking) | accessed | RRF formula and k = 60 |
| [LangChain PyPI](https://pypi.org/project/langchain/), [release policy](https://docs.langchain.com/oss/python/release-policy) | 28 Sep 2026 (v1.4.3) | Version, stability promise, 0.3 end of support |
| [LlamaIndex PyPI](https://pypi.org/project/llama-index/), [GitHub README](https://github.com/run-llama/llama_index) | 21 Sep 2026 (v0.14.25) | Version, company focus on LlamaParse |
| [Container Apps billing](https://learn.microsoft.com/en-us/azure/container-apps/billing) | 9 Dec 2025 | Free grant, scale to zero, idle billing |
| [Container Apps Dapr overview](https://learn.microsoft.com/en-us/azure/container-apps/dapr-overview) | 12 Feb 2026 | Supported pub/sub brokers |
| [Service Bus pricing](https://azure.microsoft.com/en-us/pricing/details/service-bus/) | accessed | Basic tier has no topics |
| [NATS server GitHub](https://github.com/nats-io/nats-server) | accessed | Licence, CNCF |
| [Keycloak releases](https://github.com/keycloak/keycloak/releases) | 5 Aug 2026 (v26.7.1) | Latest version |
| [Microsoft Entra pricing](https://www.microsoft.com/en-us/security/business/microsoft-entra-pricing) | accessed | External ID free for 50,000 monthly users |
| [Auth0 pricing](https://auth0.com/pricing) | accessed | Free plan limits |
| [Supabase pricing](https://supabase.com/pricing) | accessed | Free plan limits, pausing |
| [Langfuse GitHub](https://github.com/langfuse/langfuse), [Langfuse pricing](https://langfuse.com/pricing) | accessed | Licence, self-hosting needs, Hobby plan, EU region |
| [Grafana Cloud pricing](https://grafana.com/pricing/) | accessed | Free tier limits |
| [OpenTelemetry GenAI conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) | accessed | Moved to a separate repository; stability status not shown |
| [Ragas PyPI](https://pypi.org/project/ragas/) | 13 Jan 2026 (v0.4.3) | Licence and version |
| [MDN BarcodeDetector](https://developer.mozilla.org/en-US/docs/Web/API/BarcodeDetector) | accessed | Experimental, limited availability |
| [barcode-detector polyfill](https://github.com/Sec-ant/barcode-detector) | accessed | ZXing-C++ WebAssembly fallback |
| [MDN SpeechRecognition](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition) | accessed | Limited support; audio sent to a server in Chrome by default |
| [OpenAI Whisper](https://github.com/openai/whisper) | accessed | Licence, model sizes and VRAM |
| [Anthropic: Contextual Retrieval](https://www.anthropic.com/news/contextual-retrieval) | 19 Sep 2024 | Measured gains from chunk context, BM25 and reranking |
| [OWASP LLM01 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/) | 2025 | Injection mitigations |

**Not found in the research:** a benchmark of LLMs on Dutch or French repair instructions; a solid French retrieval comparison of the embedding candidates; any Dutch or French reranker results.

## 2. Market and competitor research (16 October 2026)

Used in [Market & Competitor Analysis](../02%20Analysis/Market%20&%20Competitor%20Analysis.md).

- [Apex Timing – kart maintenance](https://apex-timing.com/en/rental-karting-software-solution-c24.html)
- [SODISCAN for SODI electric karts](https://www.sodikart.com/en-gb/news/informations/sodiscan-software-for-sodi-electric-karts-69.html)
- [BMI Leisure – timing software for karting](https://www.bmileisure.com/en/features/timing-software-for-karting)
- [MaintainX vs Limble pricing (Reliamag)](https://reliamag.com/cmms/maintainx-vs-limble/)
- [MaintainX – search asset manuals with AI](https://help.getmaintainx.com/search-asset-manuals-with-maintainx-copilot)
- [UpKeep pricing guide (Fabrico)](https://www.fabrico.io/blog/upkeep-pricing-guide-2026-costs-plan-limits-hidden-fees/)
- [MECH AI on Capterra](https://www.capterra.com/p/10044904/MECH-AI/)
- [Aquant pricing (Costbench)](https://costbench.com/software/field-service-management/aquant/)
- [Valcon – RAG chatbot for 14,000 technicians](https://valcon.com/case-studies/driving-accuracy-and-speed-with-an-enterprise-rag-chatbot-for-14000-technicians/)
- [NotebookLM free vs paid (FreeAcademy)](https://www.freeacademy.ai/blog/notebooklm-free-vs-plus-2026)

## 3. Retrieval techniques (16 October 2026)

- [athina-ai/rag-cookbooks](https://github.com/athina-ai/rag-cookbooks): the 13 techniques compared in [Retrieval technique choice](../04%20RAG%20and%20AI/Retrieval%20technique%20choice.md).

- A YouTube comment by @luciderIamI ranking six RAG improvements, with replies about GraphRAG and RLM, shared by Senne on 2 November 2026. Compared in [Retrieval technique choice](../04%20RAG%20and%20AI/Retrieval%20technique%20choice.md) and recorded in [ADR-22 Relevance check also ranks, cross-references are followed, one retry before refusing](../10%20Decision%20Log/ADR-22%20Relevance%20check%20also%20ranks,%20cross-references%20are%20followed,%20one%20retry%20before%20refusing.md). Background: Microsoft Research GraphRAG; "Lost in the Middle" (Liu et al., 2023); Self-RAG (Asai et al., 2023); Recursive Language Models (Zhang and Khattab, MIT, 2025).

## 4. Fact-checks for the outside reviews (24 and 27 October 2026)

- [Azure for Students](https://azure.microsoft.com/free/students/): $100 for 12 months, no card, renewable; 750 free hours a month of PostgreSQL Flexible Server B1ms plus 32 GB for 12 months.
- [Azure free services](https://azure.microsoft.com/en-us/pricing/free-services): the same B1ms allowance.
- [Bytebase price list for Azure Flexible Server B1ms](https://www.bytebase.com/dbcost/azure-flexible/instance/B1ms/): about $15 a month in West Europe.
- [Microsoft Q&A, July 2026: Azure for Students unable to deploy any Azure OpenAI model](https://learn.microsoft.com/en-us/answers/questions/5949792/azure-for-students-unable-to-deploy-any-azure-open)
- [Microsoft Q&A: Azure AI Foundry quota insufficient for students](https://learn.microsoft.com/en-ie/answers/questions/2224916/azure-ai-foundry-quota-insufficient-issues-student)
- [Azure OpenAI quotas and limits (August 2026)](https://learn.microsoft.com/en-us/azure/foundry/openai/quotas-limits): Azure for Students listed as N/A for batch quota.
- [Fedora discussion: Docling memory crash](https://discussion.fedoraproject.org/t/docling-memory-crash-std-bad-alloc-while-parsing-multiple-pdfs-fix/185597): memory problems on big batches.

## 5. Other checks

- Claude pricing ([platform.claude.com pricing](https://platform.claude.com/docs/en/about-claude/pricing), 10 October 2026): Haiku 4.5 at $1 / $5 and Haiku 5.5 at $0.10 / $0.50 per million tokens. Used in [Answer model (LLM)](../04%20RAG%20and%20AI/Answer%20model%20%28LLM%29.md) and [Repair videos](../08%20Parked%20and%20Future%20Ideas/Repair%20videos.md).
- [Claude vision docs](https://platform.claude.com/docs/en/build-with-claude/vision): image limits, used in [Repair videos](../08%20Parked%20and%20Future%20Ideas/Repair%20videos.md).
- 3D tools (24 October 2026): glif.app, Meshy, TRELLIS and Hunyuan3D, checked on their own sites. See [3D exploded view](../06%20Design%20and%20Prototypes/3D%20exploded%20view.md).
- Cloudflare Zero Trust free plan "best for teams under 50 users" (cloudflare.com, October 2026). Considered for an outside login; not needed since MechAi is only reachable on the internal network.
- [supercube.com](https://supercube.com): the content of the demo case (AR karting, venues, identical karts).

## 6. Supercube documents (6 November 2026)

These are private company documents. Copies are in the project files under `source-docs/`, never in git.

- OTL Italia, *KART STORM – User and Maintenance Handbook*, file `STORM_HANDBOOK_V13_ENG_01082017.pdf` (footer "rev 12 IT 01-08-2017"), 89 pages, English. The source of the chatbot. See [Handbook ingestion and parsing](../04%20RAG%20and%20AI/Handbook%20ingestion%20and%20parsing.md).
- Supercube GraphQL schema, files `base.graphqls` and `mechanic.graphqls` (pod status, alerts, broken/repaired mutations, diagnostics, live subscriptions). See [Supercube integration (GraphQL)](../03%20Architecture/Supercube%20integration%20%28GraphQL%29.md).

## 7. Decisions of 6 November 2026

> [!IMPORTANT]
> The figures below are from the team's general knowledge and have not yet been checked on the pages themselves. They must be verified before they go into the final report.

- OpenAI API pricing page (openai.com/api/pricing): `text-embedding-3-small` at about $0.02 per million tokens; speech-to-text at roughly $0.003 to $0.006 per minute. To be re-checked when the models are picked. Used in [Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md).
- OpenAI's statement that API data is not used for training by default (openai.com, enterprise privacy page). To be re-checked before go-live. Used in [Answer model (LLM)](../04%20RAG%20and%20AI/Answer%20model%20%28LLM%29.md).
- Docker Compose documentation (docs.docker.com/compose) and the `pgvector/pgvector` image on Docker Hub. Used in [Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md).
- PWA requirements: installation, camera and microphone need a secure context (HTTPS or localhost), per MDN Web Docs. Used in [Hosting and deployment](../03%20Architecture/Hosting%20and%20deployment.md).
