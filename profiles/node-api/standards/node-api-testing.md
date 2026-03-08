# Node.js API Testing Standards

## Integration Testing
- Use Supertest for HTTP-level integration tests
- Test the full request/response cycle: routing → validation → logic → response
- Test both success and error paths for every endpoint

## Test Database
- Use an isolated test database (separate from dev)
- Reset database state between test suites (truncate or migrate fresh)
- Use test containers (testcontainers) for CI — spin up real PostgreSQL

## Test Data
- Use factory functions to generate test data (avoid hardcoded fixtures)
- Factories should produce valid data by default with optional overrides
- Example: `createUser({ email: 'test@example.com' })` fills in all other required fields

## Error Path Testing
- Test 400 responses for invalid input
- Test 401/403 for unauthorized/forbidden access
- Test 404 for missing resources
- Test 409 for conflict scenarios (duplicate entries)
- Test 500 handling (verify errors are logged, response is safe)

## Contract Testing
- Define API contracts (OpenAPI spec or shared types)
- Validate responses match contract schema in tests
- Consumer-driven contract tests for microservice boundaries

## Load Testing
- Use k6 for load testing critical endpoints
- Define baseline performance metrics (p95 response time, throughput)
- Run load tests before major releases or infrastructure changes
- Store load test scripts in `tests/load/`
