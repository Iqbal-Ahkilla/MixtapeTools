# Skills for Claude Code

This directory documents the **Claude Code skills** included in this repo. Skills are invocable commands that Claude Code can execute — specialized workflows you trigger with a slash command.

The actual skill files that Claude reads live in `.claude/skills/` (a hidden directory). This directory exists so you can browse and understand what's available, see examples of output, and learn how to install them in your own projects.

---

## What Are Claude Code Skills?

A **skill** is a markdown file (`.claude/skills/<name>/SKILL.md`) with YAML frontmatter that tells Claude Code what the skill does, what tools it can use, and how to invoke it. The skill name becomes a `/slash-command`. Skills encode complex, multi-step workflows into a single command.

---

## Available Skills

| Skill | Command | Description |
|-------|---------|-------------|
| [**Split-PDF**](split-pdf/) | `/split-pdf` | Download, split, and deep-read academic papers. You must specify the paper (path or search query) — Claude can't search for a paper it doesn't know exists. |

---

## How to Use These Skills in Your Own Projects

1. **Clone this repo** (or copy the `.claude/skills/` directory)
2. Place the `.claude/skills/` folder in your project root
3. Open Claude Code in that project
4. Type the slash command (e.g., `/split-pdf`)

Claude Code automatically discovers skills in `.claude/skills/`. No configuration needed beyond having the files in the right place.

---

## Adding New Skills

To create a new skill, add a directory under `.claude/skills/` with a `SKILL.md` file:

```
.claude/skills/
└── your-skill-name/
    └── SKILL.md
```

The SKILL.md needs YAML frontmatter:

```yaml
---
name: your-skill-name
description: What the skill does (one sentence)
allowed-tools: Bash(python*), Read, Write
argument-hint: [what-the-user-provides]
---

# Instructions for Claude

Write imperative instructions here. Tell Claude exactly what to do,
step by step. This is not documentation for humans — it's a prompt
that Claude follows when the skill is invoked.
```

If you develop a useful skill, PRs are welcome.
