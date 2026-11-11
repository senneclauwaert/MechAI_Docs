---
tags: [parked, future]
updated: 2026-11-06
---
# Parked and future ideas

Back to [Final Work Hub](../Final%20Work%20Hub.md)

Ideas we looked at seriously and chose not to build now, and options we keep open for later. They are kept with their reasons because the jury may ask why they were left out, and some could return as future work.

## Parked or dropped

| Idea | Status | Why |
| --- | --- | --- |
| Repair videos turned into searchable steps | Parked (10 Oct 2026); maybe a few videos later | Realistic, but out of scope for now. See [Repair videos](Repair%20videos.md) |
| QR or barcode scanning | Dropped (24 Oct 2026) | Picking from a list or searching is enough for one fleet of identical karts ([ADR-13 No QR codes](../10%20Decision%20Log/ADR-13%20No%20QR%20codes.md)) |
| An outside login service in front of the app | Not needed | MechAi is only reachable on Supercube's internal network; the `auth` module allows Supercube's own login later |
| Camera stock counting | Future work | Needs object detection trained on photos of our own parts |
| Predictive maintenance | Future work | Needs months of history per kart, which does not exist yet |
| Customer-facing features (bookings, timing, the AR game) | Out of scope | Supercube's other systems handle those |

## Semester 2 candidates

| Idea | Note |
| --- | --- |
| 3D exploded view | [3D exploded view](../06%20Design%20and%20Prototypes/3D%20exploded%20view.md) |
| Photo questions in the chat ("what is this part?") | Needs a vision-capable model; the chat and photo issues must work first |
| Step-by-step mode with read-aloud | Part of [Voice input and hands-free use](../05%20Features/Voice%20input%20and%20hands-free%20use.md) |
| The assistant answers stock and history questions | Would route those questions to SQL instead of the handbook |
| A fleet overview of Supercube's alerts | Uses `podAlertsSummary` ([Supercube integration (GraphQL)](../03%20Architecture/Supercube%20integration%20%28GraphQL%29.md)) |

## Options kept open for later

| Option | When it would make sense |
| --- | --- |
| **Kubernetes** instead of Docker Compose | If Supercube's IT already runs Kubernetes |
| **MinIO** instead of the file volume | If files must live on another machine; only the `storage` module changes |
| **LangChain or LangGraph** for the RAG code | If the pipeline grows into flows with loops and branches ([Framework choice](../04%20RAG%20and%20AI/Framework%20choice.md)) |
| **Supercube's own AI account** instead of ours | If Supercube has a contract; only the `LLMClient` configuration changes |
| **Supercube's own login** in front of MechAi | If Supercube integrates MechAi into its systems; only the `auth` module changes |
| **More venues** | The venue field already exists on karts and shelves |
