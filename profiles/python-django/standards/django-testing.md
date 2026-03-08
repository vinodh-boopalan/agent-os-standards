# Django Testing Standards

## Framework
- Use pytest + pytest-django as the test runner
- Configure in `pyproject.toml` (not `setup.cfg`)
- Use `--reuse-db` in local development for faster test runs

## Test Data
- Use Factory Boy for test data generation
- Define factories for all models: `UserFactory`, `OrderFactory`, etc.
- Factories produce valid objects by default with optional overrides
- Never use Django fixtures (JSON/YAML) — factories are more maintainable

## API Testing
- Use DRF's `APIClient` for endpoint testing
- Test all HTTP methods and status codes for each endpoint
- Test authentication and permission classes explicitly
- Test pagination, filtering, and ordering

## Test Organization
- Separate unit tests from integration tests
- Unit tests: test services, utils, model methods in isolation
- Integration tests: test full request/response cycle through views
- Place tests in `tests/` directory within each app:
  ```
  apps/users/tests/
  ├── test_models.py
  ├── test_services.py
  ├── test_views.py
  └── factories.py
  ```

## Coverage
- Minimum coverage: 80%
- Run coverage in CI: `pytest --cov --cov-fail-under=80`
- Exclude migrations and settings from coverage reports

## Mocking
- Use `responses` library to mock external HTTP calls
- Use `unittest.mock.patch` for internal dependencies
- Mock at the boundary — don't mock internal implementation details
- Freeze time with `freezegun` for time-dependent tests
