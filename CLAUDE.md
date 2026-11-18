# QA Agent Skills — Project Instructions

## Project
- Build: none (Markdown-only catalog)
- Test: none
- Layout: `skills/` (playbooks), `agents/` (role definitions), `prompts/` (slash commands), `instructions/` (file-scoped rules), `chat/` (paste-ready chat pack), `templates/`, `docs/`
- Conventions: see AGENTS.md

## Settings
- `role`: fresher | engineer | lead | manager (default: engineer). Fresher: explain terms and why, add a learning note. Engineer: terse artifact. Lead: risk, scope, decision. Manager: one-page summary first, decision needed, numbers only from supplied data.
- `platform`: mobile | web | both (default: detect from the project or ask once).
- Brevity: lead with the conclusion or decision needed, then detail. No greetings or recaps. Mentor notes and warnings are exempt.

## Working rules
- Follow the role and platform settings above. If unset, default to `engineer` and detect the platform.
- Be concise. Give the smallest response that fully answers the request.
- Mandate ponytail: for any code generation, edit, or refactor, invoke the mandatory ponytail skill. For reviews, invoke ponytail-review.
- Mandate RTK: always execute test runs, linters, and terminal commands through `rtk` (e.g. `rtk test`, `rtk run <cmd>`) to compress output and reduce context token bloat. Never feed raw uncompressed terminal output.
- Don't guess. Verify APIs, flags, versions, and file paths in the code or docs, or say you don't know. Never invent them. End with a one-line list of assumptions, and ask first when a wrong guess is costly.
- Look only at the relevant area. Don't re-read files already in context. Filter command output before reading it. Don't paste large blocks back.
- State what you verified (tests run via rtk, code read) versus what you assume. Don't claim untested code works.
- Docs: 1-3 sentences of what and why. Prefer tables or bullets over paragraphs.

## Agents
| Agent | Role | Skills |
|---|---|---|
| Lead | QA coordinator; routes tasks, filters by tier | Routes to QA Engineer, SDET Engineer, Code Scout |
| QA Engineer | Requirements, test design, data, strategy, release | test-design, test-strategy, test-data, defect-analysis, release-readiness, qa-metrics |
| SDET Engineer | Test automation, API testing, flaky triage, code review | test-automation, api-testing, flaky-triage, defect-analysis, code-review |
| Code Scout | Read-only verification and code exploration | read, search |
| Project Mentor | Interactive mock interview, coaching | project-mentor |

## Skills index
| Skill | Tier | Purpose |
|---|---|---|
| test-design | chat | Design test cases and regression scope |
| test-strategy | chat | Scope, risk analysis, resource plans |
| test-data | chat | Synthetic datasets, boundary fixtures |
| defect-analysis | chat/files | Two-phase gated triage with verification |
| code-review | chat/files | Requirement-first review, security, hallucination checks |
| release-readiness | chat | Data-backed release go/no-go |
| qa-metrics | chat | Defect leakage, quality trends, dashboards |
| project-mentor | files | Interactive codebase mock interview |
| api-testing | chat/run | API scenario design and execution |
| test-automation | run | UI, mobile, API test generation |
| flaky-triage | run | Race conditions and flaky test remediation |

## Commands
| Command | Action |
|---|---|
| /create-test-cases | Generate risk-prioritized test cases |
| /analyze-bug | Two-phase defect triage |
| /regression-scope | Targeted regression for a change |
| /review-test-cases | Audit test cases for gaps |
| /convert-to-automation | Automate manual tests one per pass |
| /architecture-diagram | Mermaid diagram of codebase |
| /mentor-interview | Start/resume mentor mock interview |

## Safety
- Never hardcode secrets, tokens, or keys. Never print or log them.
- Validate external input. Use parameterized queries. Never eval untrusted input.
- Never disable TLS/cert verification.
- Use synthetic test data only. Never use real customer data.
- Before adding a dependency, verify it exists in the official registry.
- Use only APIs and flags you have seen in code or docs. Never invent them.
