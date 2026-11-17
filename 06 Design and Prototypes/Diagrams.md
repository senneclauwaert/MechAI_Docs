---
tags: [design, diagrams]
updated: 2026-11-17
---
# Diagrams

Back to [Design and prototypes](Design%20and%20prototypes.md) · Decision: [ADR-34 The HTML prototype is the official design; diagrams as Mermaid in the vault](../10%20Decision%20Log/ADR-34%20The%20HTML%20prototype%20is%20the%20official%20design;%20diagrams%20as%20Mermaid%20in%20the%20vault.md)

All analysis diagrams live here as **Mermaid** code. Mermaid draws a diagram from a few lines of text, and both Obsidian and GitHub show it as a picture. Because the diagrams are text, they stay in sync with the decisions and can be reviewed in a pull request. The entity-relationship diagram is in [Data model](../03%20Architecture/Data%20model.md).

## 1. System architecture

```mermaid
flowchart LR
	subgraph Devices["Workshop tablets and phones (PWA)"]
		U["Operator, mechanic,<br>senior, admin"]
	end
	subgraph Server["Supercube server (Docker Compose)"]
		WEB["web<br>nginx + HTTPS"]
		API["api<br>FastAPI"]
		W["worker"]
		PG[("db<br>PostgreSQL + pgvector")]
		VOL[("files volume")]
	end
	U -->|"internal network only"| WEB
	WEB --> API
	API --> PG
	W --> PG
	API --> VOL
	W --> VOL
	API --> OAI["Mistral API (EU)"]
	W --> OAI
	API --> SC["Supercube GraphQL API"]
	W --> SC
```

## 2. Modules inside the backend

```mermaid
flowchart TB
	subgraph Backend["One backend (modular monolith)"]
		AUTH["auth"]
		FLEET["fleet"]
		ISSUES["issues"]
		INV["inventory"]
		TASKS["tasks"]
		KNOW["knowledge"]
		ASSIST["assistant"]
		SCUBE["supercube"]
		STORE["storage"]
		CORE["core: db, jobs, audit,<br>errors, events"]
	end
	ASSIST --> KNOW
	ISSUES --> FLEET
	ISSUES --> STORE
	FLEET --> SCUBE
	INV --> FLEET
	KNOW --> STORE
	TASKS -.->|"events"| ISSUES
	AUTH --> CORE
	FLEET --> CORE
	ASSIST --> CORE
```

Arrows mean "calls the `service.py` of". No module reads another module's tables.

## 3. Handbook ingestion

```mermaid
flowchart LR
	U["Admin uploads PDF"] --> F["files volume"]
	F --> J["job: ingest_document"]
	J --> D["Docling<br>(no OCR)"]
	D --> IMG["Page images (PNG)"]
	D --> S["Sections by<br>section number"]
	S --> C["Chunks +<br>context header"]
	C --> H{"Content hash<br>known?"}
	H -->|yes| R["Reuse embedding"]
	H -->|no| E["Embed new chunk"]
	R --> EV["Evaluation passes?"]
	E --> EV
	EV -->|yes| CUR["New revision<br>becomes current"]
```

## 4. Answering a question

```mermaid
flowchart TD
	Q["Question<br>(voice or text)"] --> L["Safety level in code"]
	L -->|emergency| STOP["STOP card, no AI"]
	L --> T["Translate to<br>English search terms"]
	T -->|high voltage| HV["Fixed text + pages<br>+ confirmation"]
	T -->|normal| H["Hybrid search + RRF"]
	H --> P["Parent sections"]
	P -->|below threshold| NO["Not in the handbook"]
	P --> A["Answer with citations"]
	A --> V["Verify numbers<br>and citations"]
	V --> OUT["Steps + page images"]
```

## 5. Sign-in

```mermaid
sequenceDiagram
	actor M as Mechanic
	participant P as PWA
	participant A as API (auth)
	participant D as Database
	M->>P: Opens MechAi on the workshop tablet
	P->>A: GET /auth/profiles
	A->>D: Active profiles
	A-->>P: Names, photos, roles
	M->>P: Taps own name, enters PIN
	P->>A: POST /auth/pin-login
	A->>D: Check Argon2 hash, count attempts
	alt PIN correct
		A-->>P: Session cookie (30 min idle)
	else 5th wrong PIN
		A-->>P: AUTH_PROFILE_LOCKED
	end
```

## 6. Operator to mechanic flow (the December demo)

```mermaid
sequenceDiagram
	actor O as Operator
	actor M as Mechanic
	participant APP as MechAi
	participant SC as Supercube API
	O->>APP: Report issue on kart 07 (quick pick, voice, photo)
	O->>APP: Mark kart broken
	APP->>SC: podBroken
	M->>APP: Open kart 07: issue, photo, history
	M->>APP: Ask by voice (Dutch)
	APP-->>M: Cited steps + handbook page images
	M->>APP: Take part from stock
	M->>APP: Run diagnostics (Cruise), then Stop
	APP->>SC: startPodDiagnostic / stopPodDiagnostic
	M->>APP: Log repair, mark repaired
	APP->>SC: podRepaired
	M->>APP: Thumbs up
```

## 7. Kart status (Supercube's four values)

```mermaid
stateDiagram-v2
	[*] --> GOOD
	GOOD --> BROKEN: mark broken
	GOOD --> DIAGNOSTIC: start diagnostics
	DIAGNOSTIC --> GOOD: stop diagnostics
	BROKEN --> DIAGNOSTIC: start diagnostics
	DIAGNOSTIC --> BROKEN: stop (still broken)
	BROKEN --> GOOD: mark repaired
	BROKEN --> PERMANENTLY_BROKEN: retire (admin)
	PERMANENTLY_BROKEN --> [*]
```

The exact transitions follow Supercube's system; this diagram shows how MechAi uses them. **To confirm** with Supercube.

## 8. Issue

```mermaid
stateDiagram-v2
	[*] --> open: reported
	open --> in_progress: mechanic starts
	open --> in_progress: turned into a to-do
	in_progress --> fixed: repair logged
	fixed --> [*]
```

## 9. Repair note (semester 2)

```mermaid
stateDiagram-v2
	[*] --> draft
	draft --> in_review: submit
	in_review --> approved: senior approves (PIN)
	in_review --> rejected: senior rejects
	rejected --> draft: mechanic edits
	approved --> in_review: edited
	approved --> [*]
```

## 10. Timeline

```mermaid
gantt
	title MechAi timeline (day track)
	dateFormat YYYY-MM-DD
	axisFormat %d %b
	section Semester 1
	Proposal deadline         :milestone, 2026-10-30, 0d
	Sprint 1                  :s1, 2026-11-09, 14d
	Sprint 2                  :s2, 2026-11-23, 14d
	Sprint 3 (v0.5.0)         :s3, 2026-12-07, 13d
	Self-evaluation (after Christmas) :milestone, 2027-01-11, 0d
	section Semester 2
	Build (weeks 1-2)         :2027-02-08, 14d
	Status pitch (week 3)     :milestone, 2027-02-22, 0d
	KPIs and self-evaluation (week 4) :2027-03-01, 7d
	Work week (week 5)        :2027-03-08, 7d
	Showdown (week 6)         :milestone, 2027-03-15, 0d
	Spread the Word (week 7)  :2027-03-22, 7d
```

The dates after Christmas are placeholders until the school publishes the calendar ([Planning & Deadlines](../01%20Project/Planning%20&%20Deadlines.md)).
