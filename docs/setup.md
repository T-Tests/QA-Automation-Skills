# Setup

This package provides three installation tiers. Install only the tier matching your environment capabilities:

| Tier | Environment | Skills offered | Install route |
|---|---|---|---|
| `chat` | Plain AI chat (web UI, ChatGPT, Claude.ai, etc.) | `chat` skills only | Chat route: paste single skills or `chat/qa-assistant.md` |
| `files` | IDE/agent with read-only project access | `chat` + `files` skills | Files route: read-only skills, QA Engineer, Project Mentor |
| `run` | IDE/agent with read, edit, and terminal run access | All skills (chat, files, run) | Full IDE route: all skills, agents, prompts, instructions |

## Installation routes

### Route 1: Full IDE install (`run` tier)

Best for GitHub Copilot, Claude Code, or IDE agents with workspace edit and shell execution.

1. In your repo root, create `.github/` if it does not exist:
   ```bash
   mkdir -p .github/agents .github/instructions .github/prompts .github/skills
   ```
2. Copy `agents/`, `instructions/`, `prompts/`, and `skills/` into `.github/`.
3. Copy `templates/copilot-instructions.md` to `.github/copilot-instructions.md` and fill in the bracketed project details.
4. Reload the IDE.

### Route 2: Files-only install (`files` tier)

For environments with workspace read access but without shell/execution permissions.

1. Copy only read-safe skills into `.github/skills/`:
   - `test-design`, `test-strategy`, `test-data`, `defect-analysis`, `code-review`, `release-readiness`, `qa-metrics`, `project-mentor`.
   - Exclude `run`-tier skills: `test-automation`, `api-testing`, `flaky-triage`.
2. Copy read-only agents into `.github/agents/`:
   - `qa-engineer.agent.md`, `project-mentor.agent.md`, `code-scout.agent.md`.
3. Copy prompts and instructions, then set up `.github/copilot-instructions.md`.

### Route 3: Chat route (`chat` tier)

For browser-based or standalone chat windows without repository access.

- **Option A (All-in-one):** Copy and paste the contents of `chat/qa-assistant.md` into your custom instructions, system prompt, or the start of your chat session.
- **Option B (Individual skills):** Copy and paste the specific skill file you need directly into the chat:
  - `skills/test-design/SKILL.md`
  - `skills/test-strategy/SKILL.md`
  - `skills/test-data/SKILL.md`
  - `skills/defect-analysis/SKILL.md`
  - `skills/code-review/SKILL.md` (for pasted diffs)
  - `skills/release-readiness/SKILL.md`
  - `skills/qa-metrics/SKILL.md`
  - `skills/api-testing/SKILL.md` (for scenario design only)

## Tool-specific setup guides

### Claude Code
`CLAUDE.md` is provided at the repository root and is auto-detected on startup. To install full agent and rule subdirectories:
```bash
# Optional: create specialized .claude directories
mkdir -p .claude/skills .claude/agents .claude/commands .claude/rules
cp -r skills/* .claude/skills/
for f in agents/*.agent.md; do cp "$f" ".claude/agents/$(basename "$f" .agent.md).md"; done
for f in prompts/*.prompt.md; do cp "$f" ".claude/commands/$(basename "$f" .prompt.md).md"; done
for f in instructions/*.instructions.md; do sed 's/^applyTo:/paths:/' "$f" > ".claude/rules/$(basename "$f" .instructions.md).md"; done
```

### Cursor
Zero-config: `.cursorrules` and `.cursor/rules/qa-automation.mdc` are already present in the repository root. Cursor will automatically apply QA rules, settings, agent definitions, and skills for all composer and chat prompts.

### Cline
Zero-config: `.clinerules` is located at the workspace root and automatically injected as system instructions for all Cline conversations in VS Code.

### OpenAI Codex & OpenCode
Zero-config: `CODEX.md`, `.opencode.md`, and the universal `AGENTS.md` are situated at the workspace root and automatically read by these CLI coding agents.

### Windsurf
Zero-config: `.windsurfrules` is placed at the workspace root and automatically loaded into Windsurf Cascade.

### GitHub Copilot
Pre-configured: `.github/copilot-instructions.md` is active at `.github/copilot-instructions.md`.

## Mandatory tooling setup

This package mandates **Ponytail** and **RTK** to ensure optimal token efficiency and minimal code footprint.

### 1. Ponytail (Mandatory)
Ponytail enforces strict code economy and debt tracking.
- Install the `ponytail` skill into your agent or IDE skills directory:
  ```bash
  # For GitHub Copilot:
  # Clone or copy ponytail into .github/skills/ponytail/
  git clone https://github.com/DietrichGebert/ponytail.git .github/skills/ponytail
  
  # For Claude Code:
  git clone https://github.com/DietrichGebert/ponytail.git .claude/skills/ponytail
  ```
- All test automation generation must invoke `ponytail`.
- Code reviews must run `ponytail-review`.

### 2. RTK (Mandatory)
RTK compresses test runner logs and terminal output before sending to context.
- Install the RTK CLI globally:
  ```bash
  npm install -g @rtk-ai/rtk
  # or download prebuilt binary from https://github.com/rtk-ai/rtk/releases
  ```
- Wrap all test runs and terminal commands with `rtk`:
  ```bash
  rtk npm test
  rtk pytest
  rtk run <command>
  ```

## Model-tier recommendations

Selecting the right model tier per task controls token cost while preserving quality:

- **Mechanical tasks (Cheaper/faster models):** Use lightweight models (e.g. Claude Haiku, GPT-4o-mini) for test execution, formatting, locator extraction from page source, converting single cases into existing patterns, and generating synthetic test data.
- **Cognitive tasks (Stronger models):** Use frontier models (e.g. Claude Sonnet/Opus, GPT-4o) for test strategy, architectural diagrams, defect root-cause analysis, code reviews, and release decisions.

## Verification

- **Copilot Customizations panel:** lists all installed skills, agents, prompts, and instructions.
- **QA Engineer:** ask for test cases for a login requirement. Verify output follows role and platform settings.
- **SDET Engineer:** ask for a single test case automation. Verify evidence before done and one-case-per-pass behavior.
- **Project Mentor:** send `Start`. Verify opening line, question referencing code, and absence of project summary.

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Nothing appears | Wrong folder path | Files must be under `.github/agents`, `.github/skills/<name>/SKILL.md`, etc. |
| Items still missing | Stale IDE index | Reload the IDE or reopen the project |
| Claude Code rules ignored | `applyTo` key used | Convert `applyTo:` to `paths:` in `.claude/rules/*.md` |
| Skill never triggers | Description too vague | Mention the skill by name in your prompt, or sharpen its `description` |
| Two skills load for one request | Overlapping descriptions | Narrow the `description` fields |
| Prompts don't autocomplete | Prompt files not picked up | Check the prompts folder path and your IDE's prompt-file setting |
| ponytail lines do nothing | Skill not installed | Install ponytail into `.github/skills/ponytail` or `.claude/skills/ponytail` (see Mandatory tooling setup) |
| RTK command not found | RTK CLI not installed | Install globally: `npm i -g @rtk-ai/rtk` or download prebuilt binary |
| Subagents fail in JetBrains | Preview feature limitations | Subagent coordination in JetBrains Copilot is UNVERIFIED; invoke agents directly |
