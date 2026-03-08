# Full-Stack CI/CD Standards

## Pipeline Structure
- Run CI jobs in parallel per package (web, api, shared)
- Shared package changes trigger CI for all dependent packages
- Use Turborepo/Nx remote caching to skip unchanged packages

## Deployment Order
- Deploy API before web (frontend may depend on new API endpoints)
- Use feature flags for cross-service rollouts that can't be deployed atomically
- Database migrations run before API deployment

## Change Detection
- Only build and deploy packages that have changed (or depend on changed packages)
- Use `turbo run build --filter=...[origin/main]` or Nx affected commands
- Full pipeline runs on merge to main regardless of change detection

## Environment Promotion
- dev: auto-deploy all packages on merge to main
- staging: manual promotion, full integration testing
- prod: manual promotion with approval, deploy API → run migrations → deploy web

## Contract Validation
- Validate API contract compatibility in CI before merging
- If using OpenAPI: run spectral linting and breaking change detection
- If using shared types: TypeScript compilation catches contract mismatches
