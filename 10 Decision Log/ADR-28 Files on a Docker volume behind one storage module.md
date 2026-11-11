---
id: "ADR-28"
area: "Architecture"
status: "Accepted"
date: "2026-11-06"
tags: [decision]
updated: 2026-11-06
---
# ADR-28 Files on a Docker volume behind one storage module

Back to [Decision Log](Decision%20Log.md)

**Status:** Accepted

**Context:** Issue photos, page images and the uploaded PDF must be stored somewhere on Supercube's server.

**Decision:** Files live on a Docker volume (`files`). Only the `storage` module touches it (`save_file()`, `open_file()`). The database stores the path. Photos are resized and served by the backend only after sign-in. The volume is backed up every night with the database.

**Why:** Simplest option on one server; one module to change if storage moves.

**Alternatives considered:** MinIO (S3-compatible store); storing files in the database.

**Consequences:** MinIO is the upgrade path if files must live on another machine.
