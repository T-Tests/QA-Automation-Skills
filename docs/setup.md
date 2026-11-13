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

## Claude Code setup

Claude Code uses `.claude/` instead of `.github/`. Use these commands to install:

```bash
# 1. Create directories
mkdir -p .claude/skills .claude/agents .claude/commands .claude/rules

# 2. Copy skills
cp -r skills/* .claude/skills/

# 3. Copy agents (rename .agent.md to .md)
for f in agents/*.agent.md; do
  cp "$f" ".claude/agents/$(basename "$f" .agent.md).md"
done

# 4. Copy prompts as commands (drop .prompt from filename)
for f in prompts/*.prompt.md; do
  cp "$f" ".claude/commands/$(basename "$f" .prompt.md).md"
done

# 5. Copy instructions as rules (convert applyTo to paths)
for f in instructions/*.instructions.md; do
  sed 's/^applyTo:/paths:/' "$f" > ".claude/rules/$(basename "$f" .instructions.md).md"
done

# 6. Always-on instructions
cp templates/copilot-instructions.md CLAUDE.md
```

Notes for Claude Code:
- Rules in `.claude/rules/` require a `paths:` glob list; `applyTo:` is ignored.
- `AGENTS.md` is read automatically when no `CLAUDE.md` exists (version 2.1.277+).
- Run with `--agent lead` or set `"agent": "lead"` in settings to use Lead coordinator mode.

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
| ponytail lines do nothing | Plugin not installed | Install ponytail, or ignore; the fallback rule applies |
| Subagents fail in JetBrains | Preview feature limitations | Subagent coordination in JetBrains Copilot is UNVERIFIED; invoke agents directly |
