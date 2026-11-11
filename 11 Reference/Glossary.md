---
tags: [reference, glossary]
updated: 2026-11-06
---
# Glossary

Back to [Final Work Hub](../Final%20Work%20Hub.md)

Every technical term used in this vault, explained in plain words and sorted alphabetically.

| Term | Plain meaning |
| --- | --- |
| Adapter module | A module whose only job is to talk to an outside system and translate its data into ours. Our `supercube` module is one; see [Supercube integration (GraphQL)](../03%20Architecture/Supercube%20integration%20%28GraphQL%29.md) |
| ADR | Architecture decision record: a short note that records one decision with its context, reason and alternatives. Our ADRs are in the [Decision Log](../10%20Decision%20Log/Decision%20Log.md) |
| AGPL | An open-source licence that can force you to publish your whole program's source code if you offer it as a network service |
| Alembic | A Python tool that manages database changes (migrations) as files in git |
| Apache 2.0 / MIT | Permissive open-source licences: commercial use is fine if you keep the licence notice |
| API / API key | A way for code to use a service. The key is a secret password that also bills your account; never put it in code or on GitHub |
| API gateway | One front door that receives all requests and forwards them to the right service. We don't need one |
| AR karting | Augmented-reality karting: drivers wear a headset and race on a "gaming floor" with virtual elements. What Supercube runs |
| Argon2 | A deliberately slow hashing method for passwords and PINs, so a stolen database can't easily be cracked |
| Audit log | A table that records who did what and when (status changes, diagnostics, approvals, stock changes) |
| BA4 / BA5 | Belgian qualification levels for working on electrical installations. Which tasks need which level is Supercube's call |
| BM25 / full-text search | Classic keyword search that scores documents by how often the query words appear |
| BMS | Battery management system: the electronics that protect and monitor the battery |
| CC-BY-NC | A licence that forbids commercial use |
| Chunk / chunking | A small piece of a document that is searched on its own, and the act of cutting documents into such pieces |
| Chunk overlap | Repeating a bit of text between neighbouring chunks, so a sentence cut in half isn't lost |
| CI/CD | Continuous integration and deployment: automatic tests and deployment on every change |
| Citation | The handbook section and page an answer step comes from, shown so the mechanic can check it |
| Citation verification | Code that checks every cited source was really retrieved and really contains the claim |
| Container / Docker | A container packs a program with everything it needs, so it runs the same on every machine. Docker is the tool that builds and runs containers |
| Content hash | A short fingerprint of a text. If the text doesn't change, the hash doesn't change, so its embedding can be reused |
| Context (window) | Everything sent to the LLM in one call: instructions, sources and question, measured in tokens |
| Context compression | Cutting retrieved text down to the sentences that look relevant before sending it to the LLM. We don't do it, because it could cut out a safety warning |
| Context header | A line such as "Storm handbook > 5.3 > pages 38-42" put in front of a chunk before embedding, which makes search better |
| CORS | A browser rule that decides which websites may call our API; we allow only our own frontend |
| Cosine distance | A way to measure how similar two vectors are, by the angle between them |
| Cross-encoder | A small model that reads the question and one search result together and gives a relevance score. The usual kind of reranker |
| Cross-reference link | A link from one section of the handbook to another that it mentions ("see section 5.3"), so both can be sent together (ADR-22) |
| Dense / sparse vector | Dense: a full list of numbers capturing meaning. Sparse: mostly zeros, with weights for specific words |
| Diagnostics / speed mode | A test run of a kart in Supercube's system. MechAi offers the same speed modes as the operator app: Pitlane, Cruise, Boost, High boost and High brake |
| Docker Compose | A tool that starts several containers (database, API, worker, web) together from one file with one command. MechAi runs this way on Supercube's server |
| Docker volume | A storage folder managed by Docker that survives container restarts. MechAi keeps its database (`pgdata`) and files (`files`) on volumes |
| Docling | A free tool that turns PDFs and images into structured text with headings, tables and page numbers |
| Document revision | One version of a document, such as a handbook edition. Only the current revision is searched |
| Embedding | The list of numbers a model makes for a text, so similar meanings get similar numbers |
| Embedding model | The model that makes embeddings (we use OpenAI `text-embedding-3-small`) |
| Error code | A fixed, upper-case name for an error with a module prefix, such as `INVENTORY_STOCK_NEGATIVE`. See [Error handling](../03%20Architecture/Error%20handling.md) |
| Event bus / broker | Software that delivers messages such as "RepairCompleted" between services. We don't need one |
| Faithfulness | Whether every claim in an answer is supported by the retrieved sources |
| FastAPI | A Python web framework for building APIs; it generates API documentation automatically |
| GHCR | GitHub Container Registry: GitHub's free store for container images. Our CI pushes images there; Supercube's server pulls them |
| GIN index | A Postgres index that makes full-text search fast |
| GraphQL | A way to build an API with one URL where the client asks for exactly the fields it wants. Supercube's own system uses it. We keep REST for our own API; see [Supercube integration (GraphQL)](../03%20Architecture/Supercube%20integration%20%28GraphQL%29.md) |
| GraphRAG | A RAG method where an LLM first turns all documents into a network of things and their relations, then searches that network. Too heavy for one book |
| Hallucination | A confident answer that the sources don't support |
| HNSW / IVFFlat | Two kinds of vector index. HNSW is a graph (fast search); IVFFlat groups vectors in clusters (fast to build) |
| HTTPS certificate | A file that proves a website's identity and encrypts traffic. A PWA, the camera and the microphone only work over HTTPS |
| HV | High voltage, here the kart's battery system |
| Hybrid search | Running keyword search and vector search together and merging the results |
| Idempotency key / request id | A unique id sent with a request, so a retried or double-tapped request is only processed once (used for taking stock) |
| Internal network | Supercube's own network (for example the workshop Wi-Fi). MechAi is only reachable from it |
| Iterative index scan | A pgvector feature that keeps searching when a filter removes too many results |
| KPI | Key performance indicator: a measurable goal, such as recall@10 of at least 80% |
| Kubernetes | A system that runs containers across many servers. Only needed if Supercube's IT already uses it |
| LangChain | A Python library with ready-made building blocks for LLM apps. Kept open as an option; the build uses plain Python |
| LangGraph | A library for building AI flows with steps, branches and loops. Kept open as an option |
| LLM | Large language model: the model that writes text, for us a small OpenAI chat model |
| LLM-as-judge | Using an LLM to grade another LLM's answer |
| LLMClient | Our own small class around the model, so the model or provider can be swapped in one place |
| Lost in the middle | The measured effect that LLMs pay less attention to text in the middle of a long prompt than at the start or end |
| Mermaid | A way to draw diagrams from a few lines of text. Obsidian and GitHub show them as pictures; see [Diagrams](../06%20Design%20and%20Prototypes/Diagrams.md) |
| Metadata | Extra fields stored with a chunk, such as document, revision, section and page |
| Microservices | Many small, separately deployed programs that talk over the network. Not needed for us |
| MinIO | A self-hosted file store that works like Amazon S3. Our upgrade path if files must live on another machine |
| Modular monolith | One program divided internally into modules with strict borders, like microservices without the network |
| MoSCoW | A way to rank requirements: Must, Should, Could, Won't |
| MRR | Mean reciprocal rank: 1 if the right page is first, 1/2 if second, 1/3 if third, averaged |
| MTEB / MTEB-NL | Public benchmarks for embedding models; MTEB-NL is the Dutch version |
| Multi-query | Searching with several rephrasings of the question and merging the results. Called RAG Fusion in [Retrieval technique choice](../04%20RAG%20and%20AI/Retrieval%20technique%20choice.md) |
| Multimodal / vision model | A model that understands images as well as text |
| Mutation (GraphQL) | A GraphQL request that changes data, for example `podRepaired` |
| nginx | A web server. Our `web` container uses it to serve the PWA, forward `/api` to the backend and hold the HTTPS certificate |
| Obsidian Git | An Obsidian plugin that syncs a vault with a git repository; how this documentation is shared |
| OCR | Optical character recognition: reading text from an image or scan |
| OpenTelemetry | An open standard for sending traces, metrics and logs from code to a monitoring tool. Not used in the prototype; our traces live in PostgreSQL |
| Operator | The Supercube employee who receives customers and runs the sessions. In MechAi the operator reports kart problems and marks karts broken |
| Operator app | Supercube's own app for operators, used to change kart status and run diagnostics |
| Outbox pattern | Writing events to a database table in the same transaction as the data, then delivering them |
| Parent document / section | The whole heading-level piece of the book (ideally one repair procedure) that a small chunk belongs to. We search chunks but send sections to the model |
| Parsing | Turning a file such as a PDF into structured text |
| pgvector | A PostgreSQL extension that stores vectors and searches by similarity |
| Pod | Supercube's word for one kart in its own system. Each pod has an id, a status (GOOD, DIAGNOSTIC, BROKEN, PERMANENTLY_BROKEN) and live alert codes |
| Pre-commit hook | A check that runs automatically before each git commit, such as formatting the code |
| Prompt | The text sent to an LLM: instructions, sources and question |
| Prompt injection | Text in a source or input that tries to override the model's instructions |
| PWA | Progressive web app: a website that installs like an app and can use the camera and microphone. Needs HTTPS |
| Query (GraphQL) | A GraphQL request that only reads data |
| Query rewriting | Improving the question before searching, for example making a vague question precise |
| RAG | Retrieval-augmented generation: first search your own documents, then let the LLM answer using only what was found |
| Rate limit | The maximum number of requests a service accepts per minute or per hour, for example PIN attempts or questions per user |
| recall@k | The share of questions where a correct page is in the top k results |
| Reference id | The request id shown under an error message, so the team can find the matching log line |
| Reranker | A second model that reorders the top search results by reading each one together with the question |
| Retrieval | Finding the chunks closest to the question |
| Retrieval-only mode | Our fallback when the AI is down or switched off: show the relevant pages without generated steps |
| RRF | Reciprocal rank fusion: merges ranked lists by adding 1 / (60 + rank) from each list |
| ruff / Prettier / ESLint | Tools that format and check code automatically: ruff for Python, Prettier and ESLint for TypeScript |
| Safety level | The class a question falls into (emergency, high voltage, normal), decided in code. It decides what the AI may do; see [Safety rules](../04%20RAG%20and%20AI/Safety%20rules.md) |
| Self-hosting | Running software on your own (here: Supercube's) servers instead of a cloud service |
| Self-RAG | A RAG pattern where the model decides whether it needs to search, and checks its own answer against the sources |
| Speech-to-text | Turning spoken audio into text. MechAi uses an OpenAI model so mechanics can ask questions without typing |
| Storage module | The only module that reads and writes files on the volume (`save_file()`, `open_file()`) |
| Stricter level wins | Our fail-safe rule: when two safety checks disagree, the safer (stricter) level is used |
| Structured output | Asking the LLM for a fixed format such as JSON, so code can check it |
| Subscription (GraphQL) | A GraphQL request that keeps a connection (WebSocket) open, so the server pushes new data as soon as it changes |
| Token | A piece of a word (about three quarters of a word) used to measure LLM input, output and price |
| top-k | How many search results are passed on, for example the top 5 |
| Trace | A recorded timeline of one question through the code and model calls, stored in `assistant.traces` |
| tsvector | The Postgres column type that stores text prepared for full-text search |
| Vector / vector database | A list of numbers representing meaning, and the database that stores and searches them |
| Walking skeleton | The thinnest end-to-end version of a system that already works (our `v0.1.0`) |
