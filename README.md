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
  setup.md                Setup guides for Copilot, Claude Code, Cursor, Cline, OpenCode, Codex, Windsurf
  evals.md                Evaluation rubric, 8 benchmark QA tasks, and token measurement tracking
AGENTS.md                 Operational system prompt (Codex, OpenCode, Gemini, etc.)
CONTRIBUTING.md           Contributor rules and strict quality constraints
CLAUDE.md                 Claude & Claude Code project instructions
.cursorrules              Cursor AI rules (root and .cursor/rules/)
.clinerules               Cline rules for VS Code
.opencode.md              OpenCode CLI instructions
.windsurfrules            Windsurf IDE rules
.github/                  Pre-configured Copilot instructions
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

## Supported AI tools & IDEs

| Tool | Integration File | How It Loads |
|---|---|---|
| **Claude / Claude Code** | `CLAUDE.md` | Auto-detected at workspace root |
| **Cursor** | `.cursorrules` & `.cursor/rules/qa-automation.mdc` | Auto-loaded for all queries |
| **Cline** | `.clinerules` | Auto-loaded system instructions |
| **OpenAI Codex** | `CODEX.md` / `AGENTS.md` | Auto-detected instructions |
| **OpenCode** | `.opencode.md` / `AGENTS.md` | Auto-detected instructions |
| **Windsurf** | `.windsurfrules` | Auto-loaded cascade rules |
| **GitHub Copilot** | `.github/copilot-instructions.md` | Auto-loaded repo instructions |
| **ChatGPT / Web Chat** | `chat/qa-assistant.md` | Copy & paste into any chat or custom instructions |
| **JetBrains / VS Code / Neovim / Emacs** | Standard markdown & tool config files | Native file viewer & extension support |

## Quick start

Choose the install route that matches your environment:

1. **Auto-detected route (Zero setup):** For Claude Code, Cursor, Cline, Windsurf, OpenCode, and Codex, all configuration files are already in place at the repo root. Simply open the workspace in your tool.
2. **GitHub Copilot route:** `.github/copilot-instructions.md` is pre-configured. To use custom agents, prompts, and skills, link or copy `agents/`, `prompts/`, and `skills/` into `.github/`.
3. **Chat route (`chat` tier):** paste `chat/qa-assistant.md` into your AI chat session (ChatGPT, Claude web, etc.), or paste individual chat skills directly.

Detailed setup instructions: [docs/setup.md](docs/setup.md).

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

- **Mandatory Ponytail integration:** enforces the smallest correct implementation without boilerplate or speculative abstractions; catches over-engineering with `ponytail-review`.
- **Mandatory RTK runner compression:** pipes all test execution, linter runs, and terminal output through `rtk` to compress log context before feeding AI models.
- **Generate once, replay deterministically:** AI writes and debugs tests; CI executes them with zero token cost.
- **One case per pass:** prevents massive speculative code generation loops that burn context.
- **Strict brevity rules:** strips conversational fluff, pleasantries, and duplicated recaps.
- **Scoped instructions:** file-type filtering prevents code rules from loading during doc turns.
- **Model-tier advice:** guide developers to use lightweight models for mechanical tasks and frontier models for cognitive planning (see [docs/setup.md](docs/setup.md)).
- **Measurable tracking:** verify savings using the 8 fixed benchmark tasks in [docs/evals.md](docs/evals.md).

## Mandated & integrated tooling

- **[Ponytail](https://github.com/DietrichGebert/ponytail) (Mandatory):** Enforces code economy, anti-bloat constraints, and technical debt tracking (`ponytail-debt`). Mandated for all code generation, edits, and code reviews (`ponytail-review`).
- **[RTK](https://github.com/rtk-ai/rtk) (Mandatory):** CLI tool that shrinks and compresses terminal commands, test runner logs, and linter outputs before feeding into AI context. Mandated for all test execution and shell commands.

### Security scanning with SkillSpector

[SkillSpector](https://github.com/skillspector/skillspector) is a static security and permission scanner for agent skills, prompts, and instructions. Use it to audit any third-party, community, or newly authored skill before referencing or installing it:

```bash
# Install SkillSpector CLI globally
npm install -g @skillspector/cli
# or run directly with npx without installation:
npx skillspector scan ./skills

# Scan a single skill or agent definition
skillspector scan skills/test-automation/SKILL.md
skillspector scan agents/sdet-engineer.agent.md

# Scan all skills, instructions, and agents across the repo
skillspector scan skills/ instructions/ agents/

# Strict mode: exit with non-zero code on security warnings or excessive tool requests
skillspector scan --strict ./skills
```

**What it audits:**
- **Prompt injections & jailbreaks:** hidden system overrides and malicious role prompts.
- **Secret & credential harvesting:** attempts to read or log `.env`, SSH keys, or cloud tokens.
- **Permission escalation:** skills requesting broad shell or edit capabilities when read-only suffices.
- **Typosquatted dependencies:** unverified package recommendations.

### Recommended optional tools (not bundled)
- [tapflow](https://github.com/tapflow/tapflow): mobile simulator streaming and no-LLM flow runner (v0.x, experimental runner and MCP; iOS requires macOS and Xcode).

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
- [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail): code-generation skill integration order.

## License

[MIT](LICENSE). Free to use, modify, and distribute.
