# Architecture Standards

## Architecture Decision Records (ADRs)
- Create an ADR for every major technical decision
- Store in `architecture/decisions/` with format: `NNNN-title-of-decision.md`
- ADR template:
  - **Title** — Short descriptive name
  - **Status** — Proposed | Accepted | Deprecated | Superseded
  - **Context** — Why is this decision needed?
  - **Decision** — What was decided and why
  - **Consequences** — Trade-offs, risks, follow-up actions

## C4 Model
- Use Structurizr DSL for architecture diagrams
- Maintain diagrams at System Context and Container levels minimum
- Store workspace in `architecture/workspace.dsl`
- Render diagrams in CI or via Structurizr playground
- Keep diagrams in sync with code — update when architecture changes

## Folder Structure
- Use feature-based folder structure (not layer-based)
- Group by domain/feature, not by technical role
- Shared utilities in a `shared/` or `common/` directory
- Each feature folder is self-contained: components, hooks, utils, tests

## Dependencies
- Evaluate new dependencies carefully — prefer fewer, well-maintained libraries
- Document why a dependency was chosen (in ADR if significant)
- Avoid micro-dependencies — don't install a package for trivial utilities
