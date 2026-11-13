---
name: api-testing
description: 'Design, execute, and validate API automated test cases, contract tests, and schema assertions. Use when asked to test REST, GraphQL, or gRPC endpoints, validate payloads, or verify HTTP responses. Keywords: API testing, endpoint test, REST test, payload validation, contract test, status code.'
compatibility: 'Works in chat for test case design. Needs project files and a shell to execute requests or test suites.'
---

# API Testing

Needs project files and a shell to execute tests. In plain chat, provide the API spec or endpoint schema to design test scenarios without execution.

Follow the role and platform settings. If unset, default to engineer and detect the platform.

Inspect project files to detect the existing API test framework (e.g. pytest, REST-assured, Supertest, Playwright API); never assume one.

## Design rules
- Validate business meaning and response payloads, never just HTTP 200/201 status codes.
- Security and auth: test expired tokens, missing bearer headers, insufficient permission roles (401 vs 403), injection strings in query params.
- Input validation: test boundary values, extra fields, missing required fields, nulls, incorrect data types (400/422).
- Data integrity: verify idempotency on PUT/DELETE, state mutation on POST, pagination cursor/limit bounds, sorting order.
- Mask secrets: read API keys and tokens from environment variables; never hardcode credentials.

## Execution rules (run tier)
- Evidence before done: execute the request or test suite and show status code, response snippet, and duration before calling work done.
- If unable to run in the current environment, state "not run".

## Platform specifics
- Mobile: app-version compatibility headers, token refresh flows, payload compression (gzip), offline retry queue behavior.
- Web: CORS headers, browser cookie session management, CSRF token validation, cache-control headers (ETag, 304 Not Modified).
