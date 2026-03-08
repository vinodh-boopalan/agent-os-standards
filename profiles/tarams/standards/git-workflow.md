# Git Workflow Standards

## Branching Strategy
- Trunk-based development — `main` is always deployable
- Short-lived feature branches (< 2 days)
- Branch naming: `feat/<ticket>-<short-desc>`, `fix/<ticket>-<short-desc>`, `chore/<short-desc>`
- No direct pushes to `main` — all changes via PR

## Commits
- Use conventional commits: `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`, `ci:`
- Subject line: imperative mood, < 72 characters
- Body: explain *why*, not *what*

## Pull Requests
- PR description must include: summary of changes, test plan, screenshots (if UI)
- At least 1 reviewer required
- All CI checks must pass before merge
- Squash merge to keep history clean
- Delete branch after merge

## Pre-commit Hooks
- Use Husky + lint-staged
- Pre-commit: lint + format staged files
- Pre-push: type-check

## Code Review
- Review within 24 hours
- Focus on: correctness, security, readability, test coverage
- Use "Request changes" sparingly — prefer comments with suggestions
