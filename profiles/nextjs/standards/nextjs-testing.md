# Next.js Testing Standards

## Unit & Component Testing
- Use Vitest or Jest with React Testing Library
- Test components in isolation — mock API calls and context providers
- Test Server Components by testing their rendered output
- Avoid testing implementation details — test user-visible behavior

## API Mocking
- Use MSW (Mock Service Worker) for API mocking in tests and development
- Define mock handlers that mirror actual API contracts
- Share mock definitions between tests and Storybook (if used)

## E2E Testing
- Use Playwright for end-to-end tests
- Test critical user flows: auth, navigation, form submissions, payments
- Run E2E against preview deployments in CI
- Keep E2E suite fast (< 10 min) — test happy paths + critical edge cases

## Performance Testing
- Run Lighthouse CI in the pipeline
- Test Core Web Vitals: LCP, FID, CLS
- Set performance budgets and fail CI if exceeded

## Testing Patterns
- Test pages by rendering them with required providers and mocked data
- Test Server Actions by calling them directly with test inputs
- Test middleware by simulating request/response objects
- Use `next/test-utils` where available for framework-specific testing
