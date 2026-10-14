---
name: test-design
description: 'Design test cases and regression scope from requirements, user stories, specs, bug fixes, or code changes. Use when asked to create, review, or prioritize test cases, coverage, regression scope, or negative and boundary scenarios.'
---

# Test Design

1. Confirm intended behavior. If requirements are ambiguous, list the ambiguities and ask before generating coverage. Never invent requirements. State any assumption explicitly, and mark an expected result you couldn't derive from the requirement as TBC.
2. Map the surface: primary flows, state transitions, input and validation rules, roles and permissions, boundaries and errors, persistence and data integrity, platform differences, and security-relevant paths (authentication, input handling, sensitive data).
3. For a change or fix, also identify what changed, its direct dependencies and shared components, related flows, and nearby previously fixed defects.
4. Prioritize by risk: core flow, negative, boundary, permission, state, data integrity, regression. Skip exhaustive low-value combinations. Don't default to full regression when targeted coverage is enough.
5. Write each case as setup, action, expected result. Expected results describe observable behavior, never implementation details. One case covers one behavior.

When scoping regression, label each item: fix validation, direct, integration, platform, data, UI, or permission.

When reviewing existing cases, report missing categories, duplicates, and unclear steps, with concise corrections.
