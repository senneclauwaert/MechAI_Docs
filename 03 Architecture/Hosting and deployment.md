---
tags: [architecture, hosting, deployment, cost]
updated: 2026-11-06
---
# Hosting and deployment

Back to [Architecture](Architecture.md) · Decision: [ADR-24 Self-hosted on Supercube's servers with Docker Compose, reachable only on the internal network](../10%20Decision%20Log/ADR-24%20Self-hosted%20on%20Supercube's%20servers%20with%20Docker%20Compose,%20reachable%20only%20on%20the%20internal%20network.md)

> [!IMPORTANT]
> MechAi runs on **Supercube's own server** as a set of Docker containers started with **Docker Compose**. It is reachable only on Supercube's internal network. There is no cloud hosting. The only outside service is the OpenAI API.

## Why Docker Compose

- **Docker** packs each part of the app with everything it needs into a **container**, so it runs the same on a laptop and on the server.
- **Docker Compose** starts all containers together from one file (`compose.yaml`) with one command: `docker compose up -d`.
- **Kubernetes** runs containers across many servers. MechAi is small and runs on one server, so Compose is enough. If Supercube's IT already uses Kubernetes, the same images can be deployed there with a few extra files. **To confirm** with Supercube IT.

## The containers

| Service | Image | What it does |
| --- | --- | --- |
| `db` | `pgvector/pgvector:pg16` | PostgreSQL 16 with pgvector. Data on the volume `pgdata` |
| `api` | `ghcr.io/<org>/mechai-backend` | FastAPI. Runs the database migrations (Alembic) at start |
| `worker` | the same image, other start command | Ingestion, embeddings, Supercube sync, other background jobs |
| `web` | `ghcr.io/<org>/mechai-web` (nginx) | Serves the PWA files and forwards `/api` to `api`; holds the HTTPS certificate |

**Volumes:** `pgdata` (the database) and `files` (page images, issue photos, uploaded PDFs). Both are backed up every night.

```yaml
# compose.yaml (shortened)
services:
  db:
    image: pgvector/pgvector:pg16
    volumes: [pgdata:/var/lib/postgresql/data]
    env_file: .env
    restart: unless-stopped
  api:
    image: ghcr.io/<org>/mechai-backend:${VERSION}
    command: ["sh", "-c", "alembic upgrade head && uvicorn app.main:app --host 0.0.0.0"]
    volumes: [files:/data/files]
    env_file: .env
    depends_on: [db]
    restart: unless-stopped
  worker:
    image: ghcr.io/<org>/mechai-backend:${VERSION}
    command: ["python", "-m", "app.worker"]
    volumes: [files:/data/files]
    env_file: .env
    depends_on: [db]
    restart: unless-stopped
  web:
    image: ghcr.io/<org>/mechai-web:${VERSION}
    ports: ["443:443"]
    volumes: [./certs:/etc/nginx/certs:ro]
    depends_on: [api]
    restart: unless-stopped
volumes:
  pgdata:
  files:
```

## Network and HTTPS

- Only the `web` container opens a port (443) on the server. The database and the API are not reachable from outside the Compose network.
- MechAi is reachable only from Supercube's internal network (workshop Wi-Fi). No public URL and no device setup code are needed.
- **HTTPS is required**, even on the internal network: a PWA can only be installed, and the camera and microphone only work, over HTTPS. Supercube IT provides an internal hostname (for example `mechai.supercube.local`) and a certificate that the workshop devices trust. **To confirm** with Supercube IT.
- The server needs outgoing access to `api.openai.com` and to Supercube's API.

- **Option for phones:** an internal certificate must be installed and trusted on every device, which is awkward on personal phones. An alternative is a real subdomain (for example `mechai.supercube.com`) that points to the internal IP, with a free Let's Encrypt certificate obtained through a DNS check. It stays unreachable from outside. **To confirm** with Supercube IT.
- **Guest Wi-Fi:** the setup assumes customers' Wi-Fi is a separate network. **To confirm** with Supercube IT.

## Deployment

1. A pull request runs the checks in GitHub Actions (formatting, lint, types, tests, retrieval evaluation, Docker build).
2. A merge to `main` builds the two images and pushes them to the **GitHub container registry** (GHCR), tagged with the version and the git commit.
3. On the server, an admin sets `VERSION` in `.env` and runs `docker compose pull && docker compose up -d`. The API runs the migrations at start.
4. A smoke test calls `/api/v1/health`.

The server pulls images; GitHub never needs access to Supercube's network. See [Deployment and CI-CD](../05%20Features/Deployment%20and%20CI-CD.md).

## Secrets and configuration

- All settings live in a `.env` file on the server (or Docker secrets): database password, OpenAI key, Supercube credentials, model names, limits.
- Only `.env.example` (without values) is in git.

## Backups

- Every night: `pg_dump` of the database and a copy of the `files` volume to a location chosen by Supercube IT. Keep at least 7 days.
- A restore is tested once before the Showdown.
- **To confirm:** who runs and checks the backups ([Questions for Supercube](../01%20Project/Questions%20for%20Supercube.md)).

## Monitoring

- Every container logs JSON lines to standard output; `docker compose logs` shows them. Each line has the request id, so an error reference from the screen leads to the right line.
- `GET /api/v1/health` checks the database; Compose restarts a container that stops.
- Every question gets one trace in `assistant.traces` (question, sources, scores, prompt version, model, tokens, cost, latency, answer, feedback). Traces are kept for 90 days (proposed). No handbook text goes into the plain logs.
- **Retrieval-only mode:** if the OpenAI API is down, the app shows the relevant pages without generated steps. A recorded demo video is the backup for the jury.

## Cost

Hosting runs on Supercube's own hardware, so there is no hosting bill. The only running cost is the OpenAI API.

| Item | Estimate | Note |
| --- | --- | --- |
| Embedding the whole handbook | well under 1 cent | `text-embedding-3-small`, about $0.02 per million tokens; done once per revision |
| One repair question | a fraction of a cent | One or two calls to a small chat model, about 10,000 input and 1,000 output tokens |
| Speech-to-text | about $0.003 to $0.006 per minute of audio | Most questions are under 15 seconds |

Prices are from OpenAI's price list and must be re-checked when the models are picked.

**Cost guards:** a monthly budget limit on the OpenAI project, a question limit per user (start: 30 per hour), a daily cap in config, a cap on answer length, a retry limit of 3 for jobs, and an admin switch that turns AI answers off.

## Server requirements (estimate)

- 2 CPU cores, 4 GB RAM and 20 GB disk are enough for the containers and one handbook. Docling uses the most memory during ingestion. **To confirm** with Supercube IT.
- No GPU is needed: the AI runs at OpenAI.

## Later options

- **Kubernetes** manifests, if Supercube IT uses Kubernetes.
- **MinIO** (a self-hosted file store with the same interface as Amazon S3) instead of the volume, if files must live on another machine. Only the `storage` module changes.
- Integration behind Supercube's own login. Only the `auth` module changes.
