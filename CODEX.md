# QA Agent Skills — Codex Instructions

This repository is a catalog of Markdown-based QA skills, agents, prompts, and instructions for AI coding assistants.

## Settings
- `role`: fresher | engineer | lead | manager (default: engineer). Fresher: explain terms and why, add a learning note. Engineer: terse artifact. Lead: risk, scope, decision. Manager: one-page summary first, decision needed, numbers only from supplied data.
- `platform`: mobile | web | both (default: detect from the project or ask once).
- Brevity: lead with the conclusion or decision needed, then detail. No greetings or recaps.

## Working rules
- Follow the role and platform settings above. If unset, default to `engineer` and detect the platform.
- Be concise. Give the smallest response that fully answers the request.
- Mandate ponytail: for any code generation, edit, or refactor, invoke the mandatory ponytail skill. For reviews, invoke ponytail-review.
- Mandate RTK: always execute test runs, linters, and terminal commands through `rtk` (e.g. `rtk test`, `rtk run <cmd>`) to compress output and reduce context token bloat. Never feed raw uncompressed terminal output.
- Don't guess. Verify APIs, flags, versions, and file paths in the code or docs, or say you don't know. Never invent them.
- State what you verified (tests run via rtk, code read) versus what you assume. Don't claim untested code works.
- Docs: 1-3 sentences of what and why. Prefer tables or bullets over paragraphs.

## Agents
| Agent | Role | Definition |
|---|---|---|
| Lead | QA coordinator; routes to specialists | `agents/lead.agent.md` |
| QA Engineer | Requirements, test design, data, strategy | `agents/qa-engineer.agent.md` |
| SDET Engineer | Test automation, API, flaky triage | `agents/sdet-engineer.agent.md` |
| Code Scout | Read-only verification | `agents/code-scout.agent.md` |
| Project Mentor | Mock interview coaching | `agents/project-mentor.agent.md` |

## Skills
| Skill | Tier | Playbook |
|---|---|---|
| test-design | chat | `skills/test-design/SKILL.md` |
| test-strategy | chat | `skills/test-strategy/SKILL.md` |
| test-data | chat | `skills/test-data/SKILL.md` |
| defect-analysis | chat/files | `skills/defect-analysis/SKILL.md` |
| code-review | chat/files | `skills/code-review/SKILL.md` |
| release-readiness | chat | `skills/release-readiness/SKILL.md` |
| qa-metrics | chat | `skills/qa-metrics/SKILL.md` |
| project-mentor | files | `skills/project-mentor/SKILL.md` |
| api-testing | chat/run | `skills/api-testing/SKILL.md` |
| test-automation | run | `skills/test-automation/SKILL.md` |
| flaky-triage | run | `skills/flaky-triage/SKILL.md` |

## Commands
| Command | Prompt file |
|---|---|
| /create-test-cases | `prompts/create-test-cases.prompt.md` |
| /analyze-bug | `prompts/analyze-bug.prompt.md` |
| /regression-scope | `prompts/regression-scope.prompt.md` |
| /review-test-cases | `prompts/review-test-cases.prompt.md` |
| /convert-to-automation | `prompts/convert-to-automation.prompt.md` |
| /architecture-diagram | `prompts/architecture-diagram.prompt.md` |
| /mentor-interview | `prompts/mentor-interview.prompt.md` |

## Safety
- Never hardcode secrets, tokens, or keys.
- Validate external input. Use parameterized queries.
- Never disable TLS/cert verification.
- Use synthetic test data only.
- Before adding a dependency, verify it exists in the official registry.
- Use only APIs and flags seen in code or docs. Never invent them.
