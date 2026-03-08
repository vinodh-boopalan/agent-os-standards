# Code Quality Standards

## TypeScript
- Enable `strict: true` in all TypeScript projects
- Never use `any` — prefer `unknown`, generics, or explicit types
- Enable `noUncheckedIndexedAccess` where possible

## Linting & Formatting
- ESLint and Prettier must be configured and enforced in CI
- No warnings allowed in CI — treat warnings as errors
- Use `@typescript-eslint/recommended` as baseline

## Naming Conventions
- **Variables & functions:** camelCase
- **Components & classes:** PascalCase
- **Files & directories:** kebab-case
- **Constants:** UPPER_SNAKE_CASE
- **Types & interfaces:** PascalCase (no `I` prefix)

## Code Rules
- No `console.log` in production code — use a structured logger
- Prefer named exports over default exports
- Enforce import ordering: external → internal → relative → types
- No magic numbers — extract to named constants
- No nested ternaries — use early returns or `if/else`
- Functions should do one thing and be < 50 lines
- Max file length: 300 lines (signal to split)
