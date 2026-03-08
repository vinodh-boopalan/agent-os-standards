# Security Standards

## Secrets Management
- Never commit secrets, API keys, or credentials to git
- Use `.env` files locally (always in `.gitignore`)
- Use platform secret managers in CI/CD and production (GitHub Secrets, AWS SSM, Vault)

## Dependency Security
- Enable Dependabot or Renovate for automated dependency updates
- Run dependency audit in CI — fail build on high/critical vulnerabilities
- Review and merge security PRs within 48 hours

## Authentication & Authorization
- Use established auth libraries — never roll your own crypto or auth
- Implement least privilege — users and services get minimum required permissions
- Use short-lived tokens; refresh tokens stored securely
- Enforce MFA for production access

## Input Validation
- Validate all input at system boundaries (API endpoints, form submissions)
- Use schema validation libraries: zod (TS), joi (Node), Django forms/serializers (Python)
- Never trust client-side validation alone

## OWASP Top 10
- Follow OWASP Top 10 guidelines as baseline
- SQL injection: use parameterized queries / ORM — never concatenate SQL
- XSS: escape output, use framework defaults (React JSX, Django templates)
- CSRF: enable framework protections
- HTTPS enforced in all environments (including staging)

## Logging & Monitoring
- Never log secrets, tokens, passwords, or PII
- Log security-relevant events: auth failures, permission denials, input validation failures
- Set up alerts for anomalous patterns
