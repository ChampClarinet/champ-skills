# champ-skills

Personal AI engineering skills, workflows, and development philosophies for AI-assisted software engineering.

Originally based on [`9arm-skills`](https://github.com/thananon/9arm-skills), then gradually adapted to fit my own engineering style, review process, maintainability preferences, and real-world development workflows.

## Layout

Skills live under `skills/`, grouped into categories:

- `engineering/` — debugging, review, RCA, and engineering workflows
- `productivity/` — communication and workflow translation skills
- `frameworks/` — framework-specific conventions and architecture guidance
- `personal/` — personal engineering philosophies and decision-making heuristics
- `misc/` — rarely used or experimental utilities
- `in-progress/` — draft skills not yet stable
- `deprecated/` — archived or no longer used

Each skill lives in its own directory containing:

- `SKILL.md`
- optional helper scripts
- optional reference files or examples

`SKILL.md` files use YAML frontmatter:

```md
---
name: example-skill
description: Short description here.
---
```

## Philosophy

These skills are designed around a few core principles:

- Maintainability over cleverness
- Explicitness over hidden behavior
- Simplicity over unnecessary abstraction
- Consistency over novelty
- Real execution paths over theoretical correctness
- Practical workflows over ceremony
- Engineering truth over management fluff

The goal is not to automate engineering judgment away, but to help AI systems align with consistent engineering reasoning and workflows.

## Install

For Claude Code:

```bash
./scripts/link-skills.sh
```

This symlinks shippable skills into:

```txt
~/.claude/skills/
```

List all available skills:

```bash
./scripts/list-skills.sh
```

## Codex / Other AI Tools

This repository also works well as a reusable instruction library for tools such as:

- Codex
- Cursor
- Windsurf
- ChatGPT projects
- other AI coding agents

Typical usage:

```txt
Read skills/engineering/debug-mantra/SKILL.md first.

Then debug this issue.
```

Or through a global `AGENTS.md` setup.

## Reference

### Engineering

- **[debug-mantra](./skills/engineering/debug-mantra/SKILL.md)** — Structured debugging workflow: reproduce → trace the fail path → falsify hypotheses → track breadcrumbs.
- **[post-mortem](./skills/engineering/post-mortem/SKILL.md)** — Engineering-focused root cause writeup: mechanism, fix, validation, and why it slipped through.
- **[scrutinize](./skills/engineering/scrutinize/SKILL.md)** — End-to-end review of plans, PRs, and code changes with emphasis on simplicity, correctness, and real execution paths.

### Productivity

- **[management-talk](./skills/productivity/management-talk/SKILL.md)** — Rewrite engineering content for leadership, stakeholders, or cross-functional communication while preserving technical accuracy.

### Frameworks

- **[file-structure](./skills/frameworks/file-structure/SKILL.md)** — File organization rules for maintainable component and class structure.

### Personal

- **[anti-overengineering](./skills/personal/anti-overengineering/SKILL.md)** — Prefer simpler maintainable solutions over unnecessary abstractions and complexity.
- **[maintainability-first](./skills/personal/maintainability-first/SKILL.md)** — Prioritize readability, consistency, and long-term maintainability.
- **[startup-reality](./skills/personal/startup-reality/SKILL.md)** — Balance engineering quality with practical delivery constraints.
- **[db-philosophy](./skills/personal/db-philosophy/SKILL.md)** — Database philosophy focused on integrity and maintainable business-logic boundaries.
- **[human-debugging](./skills/personal/human-debugging/SKILL.md)** — Human-centered debugging focused on understanding systems and avoiding blame.

### Misc

_(none yet)_
