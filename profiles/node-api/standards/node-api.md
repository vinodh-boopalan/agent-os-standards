# Node.js API Standards

## Framework
- Fastify preferred for new projects (performance, schema validation, plugin system)
- Express acceptable for existing projects or simple APIs
- Always use TypeScript with strict mode

## API Design
- Follow REST conventions: proper HTTP methods, status codes, plural resource names
- API versioning in URL: `/api/v1/resource`
- Response envelope pattern:
  ```json
  { "data": {}, "meta": { "page": 1, "total": 100 } }
  { "error": { "code": "NOT_FOUND", "message": "Resource not found" } }
  ```

## Input Validation
- Validate all request input using zod schemas
- Validate path params, query params, and request body
- Return 400 with descriptive error messages for validation failures
- Share zod schemas between validation and TypeScript types

## Error Handling
- Use a centralized error handler middleware
- Define custom error classes (NotFoundError, ValidationError, AuthError)
- Never expose stack traces or internal details in production responses
- Log full error details server-side with structured logging

## Logging
- Use pino for structured JSON logging
- Log: request ID, method, path, status code, response time
- Correlation IDs: generate per request, propagate to downstream services
- Log levels: error (prod), warn (staging), info (dev), debug (local)

## Security
- Rate limiting on all public endpoints (express-rate-limit / @fastify/rate-limit)
- CORS configured explicitly — no wildcard in production
- Helmet for HTTP security headers (Express) or @fastify/helmet
- Health check endpoint: `GET /health` (no auth required)

## Project Structure
```
src/
├── modules/          # Feature modules
│   └── users/
│       ├── users.controller.ts
│       ├── users.service.ts
│       ├── users.schema.ts
│       └── users.test.ts
├── common/           # Shared utilities
│   ├── errors.ts
│   ├── logger.ts
│   └── middleware/
├── config/           # Configuration
└── index.ts          # Entry point
```
