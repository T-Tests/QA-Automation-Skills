# Setup

## Per repository (shared with your team)

1. In your repo root, create `.github/` if it doesn't exist. If it already exists, merge into it; don't overwrite.
2. Copy `agents/`, `instructions/`, `prompts/`, and `skills/` into `.github/`.
3. Copy `templates/copilot-instructions.md` to `.github/copilot-instructions.md` and fill in the bracketed lines.
4. Reload the IDE.

## Global (every repo on your machine)

GitHub Copilot has no account-level cloud sync for these files on an individual plan.

1. In the (JetBrains IDEA)IDE tools menu , open the Github Copilot sub menu, then Customizations.
2. Add the folder path or git repo url under file location for Instructions, Prompts, Agents, Skills, Set the scope of each item to Personal instead of Workspace. Menu names can vary.
3. The panel shows the Personal folder path. Keep that folder in a private git repo and clone it on each machine.

## Verify

- Customizations lists 5 skills, 3 agents, and 7 prompts.
- Ask for a small function in a code file. The answer should be minimal and follow `code-economy`.
- Run `/architecture-diagram`. You should get one Mermaid block.
- Pick the SDET Engineer agent and ask for a small test. Pick QA Engineer and ask for test cases.
- Pick the Project Mentor agent and send `Start`, or run `/mentor-interview`. You should get one opening line and one question about your code.

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Nothing appears | Wrong folder path | Files must be under `.github/agents`, `.github/skills/<name>/SKILL.md`, and so on |
| Items still missing | Stale index | Reload the IDE or reopen the project |
| Skill never triggers | Description too vague | Mention the skill by name in your prompt, or sharpen its `description` |
| Two skills load for one request | Overlapping descriptions | Narrow the `description` fields |
| Prompts don't autocomplete | Prompt files not picked up | Check the prompts folder path and your IDE's prompt-file setting |
| ponytail lines do nothing | Plugin not installed | Install ponytail, or ignore; the fallback rule applies |
