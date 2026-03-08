# Testing Standards

## Coverage Requirements
- New code: >= 80% coverage
- Overall project: >= 70% coverage
- Coverage checked in CI — PR blocked if below threshold

## Test Principles
- Test behavior, not implementation details
- Each test should have a single reason to fail
- Tests must be deterministic — no flaky tests in CI
- Use descriptive test names: `should <expected behavior> when <condition>`

## Mocking
- Mock external services and APIs — never hit real endpoints in tests
- Use factories or builders for test data — avoid hardcoded fixtures
- Reset mocks between tests

## Test Structure
- Arrange → Act → Assert pattern
- Group related tests with `describe` blocks
- Keep test files next to source: `foo.ts` → `foo.test.ts`

## CI Enforcement
- Tests must pass before merge — no exceptions
- Separate unit tests (fast, < 5 min) from integration/E2E (slower)
- Run unit tests on every PR, E2E on merge to main or nightly
