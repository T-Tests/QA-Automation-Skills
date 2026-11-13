# QA Agent Skills

A complete, role-aware QA package for AI coding assistants and chat environments. Designed to serve everyone in a QA team—from fresher to manager—with first-class support for mobile (Appium, XCUITest, Espresso) and web (Playwright, Selenium, Cypress). Lowers AI token cost without sacrificing the rigor of test plans, test cases, or automation code.

## What's inside

```
skills/
  test-design/            Design test cases and regression scope (chat)
  test-strategy/          Formulate scope, risk analysis, and resource plans (chat)
  test-data/              Generate synthetic datasets and boundary fixtures (chat)
  defect-analysis/        Two-phase gated triage with independent verification (chat/files)
  code-review/            Review diffs for correctness, security, and hallucinated APIs (chat/files)
  release-readiness/      Data-backed release go/no-go recommendations (chat)
  qa-metrics/             Quality metrics, defect leakage, and executive dashboards (chat)
  project-mentor/         Interactive codebase mock interview with session memory (files)
  api-testing/            API scenario design, payload assertions, and execution (chat/run)
  test-automation/        Automated UI, mobile, and API test generation (run)
  flaky-triage/           Isolate and remediate race conditions and flaky tests (run)
agents/
  lead.agent.md           Always-on QA coordinator; routes to specialists and filters by tier
  qa-engineer.agent.md    Requirements, test design, data, strategy, and release triage (read-only)
  sdet-engineer.agent.md  Test automation, API testing, flaky triage, and code review (executes tests)
  code-scout.agent.md     Read-only workspace exploration and independent verifier subagent
  project-mentor.agent.md Interactive mock interviewer coaching across fresher to senior levels
chat/
  qa-assistant.md         Condensed all-in-one chat pack with router header (for plain chat)
instructions/
  code-economy            Minimal code, existing conventions, lint and tests before "done"
  code-safety             Security, dependency verification, and accuracy rules
  concise-docs            Short, verified documentation rules
prompts/                  Seven slash commands for test workflows
templates/copilot-instructions.md   Always-on repo instructions with role & platform settings
docs/
  setup.md                Three install routes (IDE, files, chat), Claude Code, and model-tier guide
  evals.md                Evaluation rubric, 8 benchmark QA tasks, and token measurement tracking
AGENTS.md                 Contributor rules and strict quality constraints
```

## Settings every output obeys

Configured in `templates/copilot-instructions.md` and `chat/qa-assistant.md`:
- `role`: `fresher` (explains terms, adds learning notes), `engineer` (terse artifacts), `lead` (risks, trade-offs, decisions), `manager` (executive summary first, decision needed, data-backed numbers only). Default: `engineer`.
- `platform`: `mobile`, `web`, or `both` (default: auto-detected or asked once).
- **Brevity:** lead with the conclusion or decision needed, then detail. No greetings, filler, or recaps.

## Environments and skill matrix

Skills state their environment tier via the `compatibility:` frontmatter line. Install only what works in your environment:

| Skill | Tier | Main roles | Focus |
|---|---|---|---|
| `test-design` | `chat` | fresher, engineer | Functional, boundary, and regression test cases |
| `test-strategy` | `chat` | lead | Scope boundaries, risk ranking, test allocation |
| `test-data` | `chat` | engineer | Synthetic datasets, state mocks, boundary fixtures |
| `defect-analysis` | `chat` (files opt.) | engineer, lead | Two-phase gated triage; independent verification |
| `code-review` | `chat` (diff) / `files` | engineer, SDET | Requirement-first review, security checks, hallucination checks |
| `release-readiness` | `chat` | lead, manager | Data-backed release recommendation (Go / No-Go) |
| `qa-metrics` | `chat` | manager | Escape rates, defect density, quality trends |
| `project-mentor` | `files` (chat variant) | fresher and up | Codebase interview, twists, paste-forward session memory |
| `api-testing` | `chat` (design) / `run` | engineer, SDET | Payload semantics, contract tests, HTTP verification |
| `test-automation` | `run` | SDET | Framework-native tests; evidence before done; one case per pass |
| `flaky-triage` | `run` (chat variant) | SDET | Race conditions, synchronization, state pollution isolation |

## Quick start

Choose the install route that matches your environment:

1. **Full IDE route (`run` tier):** copy `agents/`, `instructions/`, `prompts/`, and `skills/` into your repo's `.github/` folder. Copy `templates/copilot-instructions.md` to `.github/copilot-instructions.md`.
2. **Files-only route (`files` tier):** copy only read-safe skills (`test-design`, `test-strategy`, `test-data`, `defect-analysis`, `code-review`, `release-readiness`, `qa-metrics`, `project-mentor`) and read-only agents (`qa-engineer`, `code-scout`, `project-mentor`).
3. **Chat route (`chat` tier):** paste `chat/qa-assistant.md` into your AI chat session, or paste individual chat skills directly.

Detailed instructions for Claude Code and global IDE setups: [docs/setup.md](docs/setup.md).

## Agents

Select an agent in your IDE's agent picker:

| Agent | Pick it for | Example request |
|---|---|---|
| **Lead** | Coordinator; routes to specialists, filters skills by tier | `Plan and coordinate testing for the new checkout release.` |
| **QA Engineer** | Requirements, test design, data fixtures, release sign-off | `Create test cases for the biometric login lock flow.` |
| **SDET Engineer** | Writing, fixing, and running automated tests | `Automate TC-04 using our existing Page Objects.` |
| **Code Scout** | Read-only code inspection and independent verifier | `Verify whether our login endpoint allows empty passwords.` |
| **Project Mentor** | Codebase mock interview from fresher to senior | `Start`, `mid exam src/tests`, or resume with state block |

## Commands (prompts)

| Command | Action |
|---|---|
| `/create-test-cases` | Generate risk-prioritized test cases from a requirement |
| `/analyze-bug` | Two-phase defect triage (stops for confirmation before fixes) |
| `/regression-scope` | Scope targeted regression for a code change |
| `/review-test-cases` | Audit test cases for coverage gaps and unclear steps |
| `/convert-to-automation` | Automate manual test cases one case per pass |
| `/architecture-diagram` | Render the codebase architecture as a Mermaid diagram |
| `/mentor-interview` | Start or resume a mentor-style mock interview |

## How it saves tokens

- **Generate once, replay deterministically:** AI writes and debugs tests; CI executes them with zero token cost.
- **One case per pass:** prevents massive speculative code generation loops that burn context.
- **Strict brevity rules:** strips conversational fluff, pleasantries, and duplicated recaps.
- **Scoped instructions:** file-type filtering prevents code rules from loading during doc turns.
- **Model-tier advice:** guide developers to use lightweight models for mechanical tasks and frontier models for cognitive planning (see [docs/setup.md](docs/setup.md)).
- **Measurable tracking:** verify savings using the 8 fixed benchmark tasks in [docs/evals.md](docs/evals.md).

## Credits

Ideas only; all content written fresh without copying third-party text or code:

- [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill): independent verification pass that actively attempts to disprove findings.
- [obra/superpowers](https://github.com/obra/superpowers): evidence before done and two-stage requirement-first code review.
- [openqa-cn/codexqa](https://github.com/openqa-cn/codexqa): intent routing table and router header concepts.
- [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman): brevity line and zero-greeting rule.
- [vectorize-io/hindsight](https://github.com/vectorize-io/hindsight): memory without a server via paste-forward session state blocks.
- [snarktank/ralph](https://github.com/snarktank/ralph) and [frankbria/ralph-claude-code](https://github.com/frankbria/ralph-claude-code): one case per pass conversion loop.
- [fugazi/test-automation-skills-agents](https://github.com/fugazi/test-automation-skills-agents) (MIT): folder layout, agent Constitution sections, WHAT + WHEN + KEYWORDS skill descriptions, and troubleshooting structure.
- Sonu Gupta, "AI Agents for Appium: How I Built Guardrails That Actually Work" and [sonugupta029/appium-ai-agents](https://github.com/sonugupta029/appium-ai-agents): two-phase gated debugging, evidence citing, and never inventing locators.
- [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail): optional code-generation skill integration order.

### Recommended optional tools (not bundled)
- [tapflow](https://github.com/tapflow/tapflow): mobile simulator streaming and no-LLM flow runner (v0.x, experimental runner and MCP; iOS requires macOS and Xcode).
- [RTK](https://github.com/rtk-ai/rtk): CLI tool that shrinks command and test runner output before feeding it to AI context.
- [SkillSpector](https://github.com/skillspector/skillspector): static security and permission scanner for agent skills.

## License

[MIT](LICENSE). Free to use, modify, and distribute.
