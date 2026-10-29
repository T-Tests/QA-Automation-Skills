# QA Agent Skills

A catalog of lean skills, agents, instructions, and prompts for AI coding assistants doing QA and test-automation work: fewer tokens, less code, fewer invented answers. Written for GitHub Copilot (VS Code and JetBrains) as plain Markdown, so it adapts to other tools.

## What's inside

```
skills/
  test-design/            Design test cases and regression scope
  defect-analysis/        Triage a bug or failure in two gated phases
  test-automation/        Write UI, API, mobile, and performance tests
  code-review/            Review a diff for correctness, security, and invented APIs
  project-mentor/         Mentor-style mock interview about a project
agents/
  qa-engineer.agent.md    Analysis and test design, no code changes
  sdet-engineer.agent.md  Automation work, verified with targeted runs
  project-mentor.agent.md Interviews and coaches you on a project, no code changes
instructions/             Scoped by file type
  code-economy            Minimal code, existing conventions, lint and tests before "done"
  code-safety             Security, dependency, and accuracy rules
  concise-docs            Short, verified documentation
prompts/                  Seven slash commands (see below)
templates/copilot-instructions.md   Short always-on repo instructions
docs/setup.md             Setup, global use, troubleshooting
AGENTS.md                 Contributor rules
```

## Quick start

1. Copy `agents/`, `instructions/`, `prompts/`, and `skills/` into your repo's `.github/`. Merge with existing folders; don't overwrite.
2. Copy `templates/copilot-instructions.md` to `.github/copilot-instructions.md` and fill in the bracketed lines.
3. Reload the IDE and open Copilot Chat.

Global setup, verification, and troubleshooting: [docs/setup.md](docs/setup.md).

## Using it

| Command | Does |
|---|---|
| `/create-test-cases` | Create focused test cases from a requirement |
| `/analyze-bug` | Analyze a defect, then stop for confirmation before any fix |
| `/regression-scope` | Scope targeted regression for a change or fix |
| `/review-test-cases` | Find coverage gaps, duplicates, and unclear steps |
| `/convert-to-automation` | Turn manual cases into automation using your framework |
| `/architecture-diagram` | Draw the codebase as a Mermaid diagram |
| `/mentor-interview` | Start a mentor-style mock interview about the open project |

Example: `/create-test-cases Users reset their password with an emailed link that expires after 15 minutes.`

### Invoke an agent

1. Open Copilot Chat (VS Code: `Ctrl+Alt+I`; JetBrains: the GitHub Copilot tool window).
2. Open the agent picker (the mode dropdown next to the chat input) and select the agent. Names appear as the `name` in each file. Don't see it? Reload the IDE and check `.github/agents/`.
3. Type your request and send it.

| Agent (picker name) | Pick it for | Example message |
|---|---|---|
| QA Engineer | Requirements, defects, test design. Doesn't change code. | `Design test cases for the login lockout after 5 failed attempts.` |
| SDET Engineer | Writing, fixing, and reviewing automation. Runs targeted tests. | `Automate TC-12 using our existing page objects.` |
| Project Mentor | Mock interview about your project. Doesn't change code. | `Start`, `mid exam`, or `junior src/tests flaky tests` |

Project Mentor settings (all optional, any order): level `junior` (default), `mid`, `senior`; mode `coach` (default) or `exam`; scope a path or `changes`; plus a focus theme. In a session, type `hint`, `skip`, `retry`, `teach me`, `harder`, `easier`, `focus on X`, `mode coach|exam`, or `end session` for the summary.

### Invoke a prompt

Type `/` in Copilot Chat, pick the command, then add your input on the same line, for example `/analyze-bug Checkout returns 500 when the cart has one item.` For `/mentor-interview mid exam src/tests`, select the Project Mentor agent first.

### Invoke a skill

Skills load on their own when your request matches their description. To force one, name it in the message: `Use the code-review skill on my current changes.` Skills: `test-design`, `defect-analysis`, `test-automation`, `code-review`, `project-mentor`.

### Instructions

`concise-docs` applies to Markdown files. `code-economy` and `code-safety` apply to `.js .ts .jsx .tsx .py .java .kt .cs .go .rb` files. They load automatically; nothing to invoke.

## Use with other tools

Skills follow the open `SKILL.md` standard. `name` and `description` are portable, so skill folders copy as-is.

| Assistant | Placement and notes |
|---|---|
| Copilot, VS Code | The `.github/` layout above. |
| Copilot, JetBrains | Same layout. GitHub release notes report support, but the author hasn't tested it. Verify in the Customizations panel. |
| Claude Code | Skills: `.claude/skills/<name>/SKILL.md`. Agents: `.claude/agents/<name>.md` (rename from `.agent.md`). Always-on: `CLAUDE.md`, or `AGENTS.md` if no `CLAUDE.md`. Scoped rules: `.claude/rules/*.md` with `paths:` instead of `applyTo:`. Prompts: `.claude/commands/<name>.md`. |
| Codex | Skills: `.agents/skills/<name>/SKILL.md` or `~/.agents/skills/`. Instructions: `AGENTS.md`. No verified equivalent for agents or prompts. |
| Antigravity | From a community guide, not official docs: skills in `.agents/skills/` or `~/.gemini/config/skills/`; rules in `.agents/rules/`; `GEMINI.md` as entry file; agents invoked by file path. |

## How it saves tokens

- The always-on template is short. Detail lives in skills, which load on demand.
- Instructions are scoped by file type, so code rules don't load for docs and the reverse.
- The template tells the assistant to look only at the relevant area, skip files already in context, and filter command output.
- Code generation uses the optional [ponytail](https://github.com/DietrichGebert/ponytail) skill when installed. Otherwise the files fall back to the smallest correct implementation.

## Design notes and limits

- `defect-analysis` stops after analysis and waits for confirmation. This is a prompt rule, not a tool-enforced gate. For hard enforcement, restrict tools in your IDE or use hooks.
- The security rules lower risk; they don't replace a dedicated security scanner.
- Rules can't prevent every invented answer. Verify what matters and run the tests.
- Agents omit `tools:` because tool names differ between IDEs. Add it for your environment if you want least-privilege.
- No build or tests: this repo is Markdown only.

## Contributing

See [AGENTS.md](AGENTS.md).

## Credits

Ideas only; no content was copied.

- [fugazi/test-automation-skills-agents](https://github.com/fugazi/test-automation-skills-agents) (MIT): folder layout, agent Constitution sections, WHAT + WHEN + KEYWORDS skill descriptions, and the troubleshooting table.
- Sonu Gupta, "AI Agents for Appium: How I Built Guardrails That Actually Work", and its companion repo [sonugupta029/appium-ai-agents](https://github.com/sonugupta029/appium-ai-agents): two-phase gated debugging, evidence citing, and never inventing locators.
- [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail): the optional code-generation skill. The fallback order in `code-economy` follows its approach.
- Also reviewed for comparison: [PramodDutta/qaskills](https://github.com/PramodDutta/qaskills) (MIT), a QA skills directory and CLI.

## License

[MIT](LICENSE). Free to use, modify, and distribute.
