# Bruno's Agentic Skills

A collection of custom skills for AI coding agents. Each skill packages specialized knowledge — design systems, workflows, conventions — into a format that agents can discover and load automatically.

Works with [Claude Code](https://docs.anthropic.com/en/docs/claude-code), [Codex CLI](https://github.com/openai/codex), and [OpenCode](https://github.com/opencode-ai/opencode).

## Available Skills

| Skill | Description |
|-------|-------------|
| [cyberpunk-frontend-design-skill](./cyberpunk-frontend-design-skill/) | A dark, terminal-inspired cyberpunk design system for building frontend UIs. Includes tokens, components, layout patterns, and production guidelines. |

## How to Install

Clone the repo first:

```bash
git clone https://github.com/brunolopes/bruno-agentic-skills.git
```

Then copy the skill you want into the right directory for your tool. You can install at **personal** level (available across all projects) or **project** level (single project only).

### Claude Code

```bash
# Personal (all projects)
cp -r bruno-agentic-skills/cyberpunk-frontend-design-skill ~/.claude/skills/

# Project-level (from your project root)
cp -r bruno-agentic-skills/cyberpunk-frontend-design-skill .claude/skills/
```

Once installed, the skill appears in the `/` menu. Type `/cyberpunk-frontend-design-skill` to invoke it manually, or just ask Claude to build a UI — the skill triggers automatically on frontend work.

### Codex CLI

```bash
# Personal (all projects)
cp -r bruno-agentic-skills/cyberpunk-frontend-design-skill ~/.agents/skills/

# Project-level (from your project root)
cp -r bruno-agentic-skills/cyberpunk-frontend-design-skill .agents/skills/
```

Codex discovers skills automatically and loads them when the task matches the skill description.

### OpenCode

OpenCode supports multiple skill directories, including Claude Code's:

```bash
# Personal (all projects)
cp -r bruno-agentic-skills/cyberpunk-frontend-design-skill ~/.config/opencode/skills/
# or
cp -r bruno-agentic-skills/cyberpunk-frontend-design-skill ~/.claude/skills/

# Project-level (from your project root)
cp -r bruno-agentic-skills/cyberpunk-frontend-design-skill .opencode/skills/
# or
cp -r bruno-agentic-skills/cyberpunk-frontend-design-skill .claude/skills/
```

OpenCode scans for `SKILL.md` files in `.opencode/skills/`, `.claude/skills/`, and `.agents/skills/` directories.

## Skill Structure

Each skill follows this layout:

```
skill-name/
├── SKILL.md              # Entry point — name, description, and instructions
└── references/           # Supporting docs the agent reads as needed
    ├── components.md
    ├── patterns.md
    └── tokens.md
```

The `SKILL.md` file uses YAML frontmatter with a `name` and `description` that tells the agent what the skill does and when to activate it. The `references/` directory holds detailed specs loaded on demand.

## License

MIT
