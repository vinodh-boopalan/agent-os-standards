# CI/CD Standards

## Pipeline (GitHub Actions)
- Every PR triggers: lint → type-check → test → build
- Steps run in order — fail fast on first error
- Cache dependencies and build artifacts between runs

## Environments
- **dev** — auto-deploy from `main` on every merge
- **staging** — manual promotion from dev, used for QA
- **prod** — manual promotion from staging, requires approval

## Versioning
- Use semantic versioning (semver): MAJOR.MINOR.PATCH
- Auto-generate version from conventional commits (semantic-release or similar)
- Tag releases in git

## Secrets & Security
- Never commit secrets — use GitHub Secrets or a vault
- Use OIDC for cloud provider authentication where possible
- Run `npm audit` / `pip audit` in CI — fail on high/critical vulnerabilities

## Deployment
- Every deployment must be reversible — document rollback procedure
- Use health checks to verify deployment success
- Notify team channel on deploy success/failure
