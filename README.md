# DeskOps

Service desk platform with an SLA engine, built during the LogicVeda Web Development internship programme (Phase 1: Ticketing Core).

> Internal project. Do not share this repository or its documents outside the programme.

## Tech stack

| Layer | Tools |
|---|---|
| Frontend | React 18, TypeScript, Vite, TanStack Query, React Hook Form, Zod, Tailwind CSS |
| Backend | Node.js 22, TypeScript, Express, Zod |
| Data | PostgreSQL, Prisma, Redis |
| Local services | Docker and docker-compose |

## Prerequisites

Install these once on your laptop:

1. **Git**: https://git-scm.com
2. **Node.js 22**: install with [nvm](https://github.com/nvm-sh/nvm) (macOS/Linux) or [nvm-windows](https://github.com/coreybutler/nvm-windows), then run `nvm install 22`
3. **Docker Desktop**: https://www.docker.com/products/docker-desktop (open it and wait until it says it is running)
4. A **GitHub account** with access to this repository

Check your setup:

```bash
node -v      # should print v22.x
docker -v
git --version
```

## Getting started

```bash
# 1. Clone the repository
git clone <REPO_URL>
cd deskops

# 2. Use the right Node version
nvm use

# 3. Create your local environment file
cp .env.example .env

# 4. Start PostgreSQL and Redis
docker compose up -d

# 5. Install dependencies
cd backend && npm install
cd ../frontend && npm install
cd ..
```

## Running the project

Open two terminals from the repository root.

**Terminal 1: backend**

```bash
cd backend
npm run dev
```

**Terminal 2: frontend**

```bash
cd frontend
npm run dev
```

## Check that everything works

| What | Where | Expected |
|---|---|---|
| Backend health check | http://localhost:4000/health | JSON response saying the service is OK |
| Frontend | http://localhost:5173 | The DeskOps page loads |
| PostgreSQL | `docker compose ps` | `db` is running |
| Redis | `docker compose ps` | `redis` is running |

If all four check out, your setup is complete. Post "setup done" in the team chat.

## Project structure

```
deskops/
  backend/        API server (routes, services, repositories)
  frontend/       React application
  docs/
    adr/          Architecture decision records (one page each)
    retros/       Retrospective notes
  docker-compose.yml
  .env.example    Template for environment variables
  .nvmrc          Node version
```

## Environment variables

Copy `.env.example` to `.env`. **Never commit `.env`.** If you add a new variable, add it to `.env.example` with a safe placeholder value in the same pull request.

## Stopping and resetting

```bash
docker compose down        # stop the services, keep the data
docker compose down -v     # stop the services and delete the local database
```

## Working agreement

- `main` is protected. Never push to it directly.
- Create a branch from `main`: `feature/<short-name>`, `fix/<short-name>`, or `docs/<short-name>`.
- Use [Conventional Commits](https://www.conventionalcommits.org): `feat: add ticket list`, `fix: handle empty comment`, `docs: update README`.
- Keep commits small and commit often.
- Open a pull request using the template (what, why, how tested, screenshots). CI must pass and one teammate must approve before merging.
- Schema changes go through Prisma migrations only.
- No secrets in Git. Production data is never used in development.
- Record any decision that could reasonably be questioned as a one-page ADR in `docs/adr/`.

## Team

| Member | Module | Platform responsibility |
|---|---|---|
| _TBD_ | _TBD_ | _TBD_ |
| _TBD_ | _TBD_ | _TBD_ |
| _TBD_ | _TBD_ | _TBD_ |
| _TBD_ | _TBD_ | _TBD_ |

Mentor: Shaurya Pandey

## Troubleshooting

| Problem | Fix |
|---|---|
| `port is already allocated` on 5432 or 6379 | Another Postgres or Redis is running on your laptop. Stop it, or change the port mapping in `docker-compose.yml` and update `.env`. |
| `docker: command not found` or "cannot connect to the Docker daemon" | Open Docker Desktop and wait until it is running. |
| Wrong Node version | Run `nvm use` in the repository root. |
| Backend cannot connect to the database | Run `docker compose ps` and confirm `db` is up. Check that `DATABASE_URL` in `.env` matches `.env.example`. |
| `npm install` fails | Delete `node_modules` and `package-lock.json` only if a teammate confirms, then retry. Otherwise ask in the team chat with the full error text. |

## Need help?

1. Ask your teammates in the team chat.
2. Post a question on the Projects page on LogicVeda.
3. Raise a blocker in the weekly check-in so the mentor is notified.