# Agent Skills | Cursor Docs

Source: https://cursor.com/docs/skills

---

# Agent Skills

Agent Skills is an open standard for extending AI agents with specialized capabilities. Skills package domain-specific knowledge and workflows that agents can use to perform specific tasks.

## What are skills?

A skill is a portable, version-controlled package that teaches agents how to perform domain-specific tasks. Skills can include scripts, templates, and references that agents may act on using their tools.

### Portable

Skills work across any agent that supports the Agent Skills standard.

### Version-controlled

Skills are stored as files and can be tracked in your repository, or installed via GitHub repository links.

### Actionable

Skills can include scripts, templates, and references that agents act on using their tools.

### Progressive

Skills load resources on demand, keeping context usage efficient.

## How skills work

When Cursor starts, it automatically discovers skills from skill directories and makes them available to Agent. The agent is presented with available skills and decides when they are relevant based on context.

Skills can also be manually invoked by typing `/` in Agent chat and searching for the skill name.

## Skill directories

Skills are automatically loaded from these locations:

| Location            | Scope               |
| ------------------- | ------------------- |
| `.agents/skills/`   | Project-level       |
| `.cursor/skills/`   | Project-level       |
| `~/.agents/skills/` | User-level (global) |
| `~/.cursor/skills/` | User-level (global) |

For compatibility, Cursor also loads skills from Claude and Codex directories: `.claude/skills/`, `.codex/skills/`, `~/.claude/skills/`, and `~/.codex/skills/`.

Each skill should be a folder containing a `SKILL.md` file:

```text
.agents/
└── skills/
    └── my-skill/
        └── SKILL.md
```

Skills can also include optional directories for scripts, references, and assets:

```text
.agents/
└── skills/
    └── deploy-app/
        ├── SKILL.md
        ├── scripts/
        │   ├── deploy.sh
        │   └── validate.py
        ├── references/
        │   └── REFERENCE.md
        └── assets/
            └── config-template.json
```

### Nested skill directories

... (full details in source)

## SKILL.md file format

Each skill is defined in a `SKILL.md` file with YAML frontmatter:

```markdown
---
name: my-skill
description: Short description of what this skill does and when to use it.
---

# My Skill

Detailed instructions for the agent.
...
```

### Frontmatter fields

| Field                      | Required | Description |
| -------------------------- | -------- | ----------- |
| `name`                     | Yes      | Skill identifier. |
| `description`              | Yes      | Describes what the skill does and when to use it. |
| `paths`                    | No       | Glob patterns that scope the skill to matching files. |
| `disable-model-invocation` | No       | When `true`, the skill is only included when explicitly invoked via `/skill-name`. |

## Scoping a skill to specific files

Use the `paths` field to limit a skill to files that match one or more glob patterns.

## Including scripts in skills

Skills can include a `scripts/` directory containing executable code that agents can run.

## Optional directories

| Directory     | Purpose |
| ------------- | ------- |
| `scripts/`    | Executable code that agents can run |
| `references/` | Additional documentation loaded on demand |
| `assets/`     | Static resources like templates, images, or data files |

## Viewing skills

To view discovered skills:

1. Open **Cursor Settings** (Cmd+Shift+J on Mac, Ctrl+Shift+J on Windows/Linux)
2. Navigate to **Rules**
3. Skills appear in the **Agent Decides** section

## Installing skills from GitHub

You can import skills from GitHub repositories via Settings > Rules > Add Rule > Remote Rule (Github).

## Migrating rules and commands to skills

Cursor includes a built-in `/migrate-to-skills` skill.

## Learn more

Agent Skills is an open standard. Learn more at [agentskills.io](https://agentskills.io).

---

## Sitemap

[Overview of all docs pages](/llms.txt)
