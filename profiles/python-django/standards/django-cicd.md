# Django CI/CD Standards

## Package Management
- Use Poetry for dependency management (preferred)
- Alternative: pip with `requirements/base.txt`, `requirements/dev.txt`
- Pin all dependency versions — no loose ranges in production

## Python Version
- Python 3.11+ required for all new projects
- Specify exact version in `.python-version` and `pyproject.toml`

## CI Pipeline (GitHub Actions)
- Pipeline order: ruff (lint) → mypy (type-check) → pytest → Docker build
- All steps must pass — fail fast on first error
- Cache pip/Poetry dependencies between runs

## Linting & Type Checking
- Use ruff for linting and formatting (replaces flake8, isort, black)
- Use mypy with strict mode for type checking
- Both enforced in CI — zero warnings policy

## Deployment
- Deploy via Docker: `python:3.11-slim` base image
- Production server: Gunicorn with Uvicorn workers (for async support)
- Run `collectstatic` in CI/Docker build — not at runtime
- Run migrations as a pre-start step in deployment (not in application code)
- Use Nginx or cloud load balancer as reverse proxy

## Database Migrations in Deploy
- Run `python manage.py migrate` as a pre-deployment step
- Migrations must be backwards-compatible (support rolling deploys)
- For breaking changes: multi-step migration (add new → migrate data → remove old)

## Health Checks
- Expose `/health/` endpoint (no auth) that checks DB connectivity
- Use for container orchestration liveness/readiness probes
