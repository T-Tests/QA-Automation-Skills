---
name: test-data
description: 'Design and generate realistic synthetic test datasets, edge-case fixtures, boundary values, and state mocks. Use when asked for test data, fixtures, mock data, boundary values, or test database seed sets. Keywords: test data, mock data, fixtures, test fixtures, synthetic data, boundary values, seed data.'
compatibility: 'Works in plain chat with pasted input.'
---

# Test Data

Follow the role and platform settings. If unset, default to engineer and detect the platform.

Deliver clean, reproducible, structured data artifacts ready for immediate test setup.

## Strategy
1. Synthetic only: never use real customer records, live credentials, or production secrets. Generate valid synthetic equivalents.
2. Boundary and edge values: include min, max, min-1, max+1, empty, null, special characters, unicode strings, and maximum allowed field lengths.
3. State lifecycle: provide paired datasets representing valid initial states, transitional states, expired/revoked states, and terminal states.
4. Relational integrity: ensure cross-entity IDs, timestamps, and foreign keys remain coherent across joined entities.
5. Formatting: output fixtures in standard structured formats (JSON, CSV, SQL insert statements, or YAML) matching the team's stack.

## Platform specifics
- Mobile: phone number formats by country code, mock GPS coordinates, device push tokens, biometrics enrollment flags, offline storage schemas (SQLite/Room/CoreData).
- Web: cookie headers, session storage mock payloads, URL query param combinations, file upload fixtures (MIME types, file size limits).

If schemas or field constraints are unspecified, list assumed data types and constraints explicitly alongside the fixtures.
