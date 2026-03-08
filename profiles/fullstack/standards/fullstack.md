# Full-Stack Standards

## Monorepo Structure
- Use a monorepo for projects with tightly coupled frontend and backend
- Recommended layout:
  ```
  packages/
  ├── web/          # Next.js or React frontend
  ├── api/          # Node.js or Django backend
  ├── shared/       # Shared types, utils, constants
  └── config/       # Shared ESLint, TSConfig, etc.
  ```
- Use Turborepo or Nx for build orchestration and caching

## Shared Types & Contracts
- Shared TypeScript types are the single source of truth for API contracts
- Alternative: OpenAPI spec generated from backend, client SDK generated from spec
- Never duplicate type definitions between frontend and backend
- Changes to shared types trigger builds in all dependent packages

## Environment Variables
- Prefix with service name: `WEB_API_URL`, `API_DATABASE_URL`
- Each package manages its own `.env` file
- Shared env vars documented in root `.env.example`

## Local Development
- Use `docker-compose` for local development (database, cache, queues)
- Single command to start all services: `turbo dev` or `docker-compose up`
- Seed scripts that set up both database and any required test data
- Document setup in root `README.md` — new developer should be running in < 15 minutes
