# React Native Testing Standards

## Unit & Component Testing
- Use Jest + React Native Testing Library (RNTL)
- Test user-visible behavior — query by text, role, testID
- Avoid testing implementation details (state, internal methods)
- Mock native modules in `jest.setup.js` or per-test as needed

## Snapshot Testing
- Use snapshots only for pure presentational components with no logic
- Keep snapshots small — snapshot individual components, not entire screens
- Review snapshot changes carefully — don't blindly update
- If a snapshot test frequently breaks from unrelated changes, replace with behavioral test

## Mocking Native Modules
- Mock `react-native` modules that aren't available in test environment
- Use `jest.mock()` for third-party native packages (camera, location, etc.)
- Create shared mock files in `__mocks__/` for commonly mocked modules
- Keep mocks minimal — only mock what the test needs

## E2E Testing
- Use Detox or Maestro for end-to-end testing
- Test critical user flows: onboarding, auth, main navigation, key features
- Run E2E on CI using emulators/simulators
- Keep E2E suite fast (< 15 min) — focus on smoke tests for critical paths

## Test Organization
- Colocate test files: `Component.tsx` → `Component.test.tsx`
- Use `describe` blocks to group by component/feature
- Separate E2E tests in `e2e/` directory at project root
- Integration tests (multi-component flows) in `__tests__/integration/`

## Performance Testing
- Profile renders with React DevTools Profiler during development
- Monitor JS thread FPS in development builds
- Set up Flashlight or custom benchmarks for critical screens
