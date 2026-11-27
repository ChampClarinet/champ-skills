# champ-skills

Personal AI engineering skills, workflows, and development philosophies for AI-assisted software engineering.

Originally based on [`9arm-skills`](https://github.com/thananon/9arm-skills), then gradually adapted to fit my own engineering style, review process, maintainability preferences, and real-world development workflows.

## Layout

Skills live under `skills/`, grouped into categories:

- `engineering/` — debugging, review, RCA, and engineering workflows
- `design/` — landing pages, UI refinement, dashboards, and data visualization
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

For Codex automatic skill discovery, link the skills into `~/.agents/skills/` with `./scripts/link-skills.sh codex`. The router composes discovered skills; it does not replace their installation.

## Agent behavior evaluations

See [manual evaluation protocol](./evals/README.md) and [initial regression cases](./evals/cases.md) for checking skill and model behavior. These are not installed skills or automated runtime tests.

## Reference

### Design

- **[landing-page-design](./skills/design/landing-page-design/SKILL.md)** — Design new conversion-focused landing pages, campaign pages and marketing heroes.
- **[unslop](./skills/design/unslop/SKILL.md)** — Audit and refine existing UI that looks generic or AI-generated.
- **[chart-selection](./skills/design/chart-selection/SKILL.md)** — Choose truthful chart types and visual encodings based on analytical questions and data shape.
- **[dashboard-design](./skills/design/dashboard-design/SKILL.md)** — Structure actionable dashboards with KPI hierarchy, panels, filters, and states.
- **[data-viz-review](./skills/design/data-viz-review/SKILL.md)** — Audit charts and dashboards for misleading presentation, data fidelity, and accessibility.

### Engineering

- **[visual-verification](./skills/engineering/visual-verification/SKILL.md)** — Verify rendered appearance when visual correctness matters to acceptance criteria.
- [verification](skills/engineering/verification/SKILL.md) — Evidence-based acceptance verification and truthful completion.
- **[skill-router](./skills/engineering/skill-router/SKILL.md)** — Compose relevant skills, resolve authority, and avoid redundant or conflicting instruction loads.
- **[agent-orchestration](./skills/engineering/agent-orchestration/SKILL.md)** — Scale planning to risk and choose an economical single- or multi-agent workflow, with bounded execution and escalation.
- **[debug-mantra](./skills/engineering/debug-mantra/SKILL.md)** — Evidence-driven debugging: establish a failure signal, trace the path, falsify hypotheses, and verify the original signal after fixing.
- **[post-mortem](./skills/engineering/post-mortem/SKILL.md)** — Engineering-focused root cause writeup: mechanism, fix, validation, and why it slipped through.
- **[scope-discipline](./skills/engineering/scope-discipline/SKILL.md)** — Keep changes within the requested outcome while allowing proportionate maintainability work.
- **[ownership-boundaries](./skills/engineering/ownership-boundaries/SKILL.md)** — Keep state, side effects, data access, dependencies, and behavior at the narrowest meaningful owner.
- **[tooling-feedback](./skills/engineering/tooling-feedback/SKILL.md)** — Treat actionable compiler, linter, language-server, and framework diagnostics on touched code as implementation feedback.
- **[scrutinize](./skills/engineering/scrutinize/SKILL.md)** — End-to-end review of plans, PRs, and code changes with emphasis on simplicity, correctness, and real execution paths.
- **[rubberduck](./skills/engineering/rubberduck/SKILL.md)** — Interactive reasoning mode that asks focused questions before touching code.
- **[reviewer](./skills/engineering/reviewer/SKILL.md)** — Review-only mode for correctness, regression, maintainability, and scope issues.
- **[minimalist](./skills/engineering/minimalist/SKILL.md)** — Prefer less code movement among equally correct and maintainable solutions.
- **[skeptic](./skills/engineering/skeptic/SKILL.md)** — Treat proposed solutions as hypotheses and challenge assumptions with evidence.
- **[archaeologist](./skills/engineering/archaeologist/SKILL.md)** — Investigate callers, history, contracts, and old constraints before changing legacy code.
- **[paranoid](./skills/engineering/paranoid/SKILL.md)** — Aggressive pre-ship verification of edge cases, failure paths, races, compatibility, and test blind spots.

- [bun-monorepo](skills/engineering/bun-monorepo/SKILL.md)
- [git-workflow](skills/engineering/git-workflow/SKILL.md)

### Productivity

- **[show-me](./skills/productivity/show-me/SKILL.md)** — Explain complex requirements, plans, and changes with the smallest effective visual representation.

- **[management-talk](./skills/productivity/management-talk/SKILL.md)** — Rewrite engineering content for leadership, stakeholders, or cross-functional communication while preserving technical accuracy.

### Frameworks

- **[file-structure](./skills/frameworks/file-structure/SKILL.md)** — File organization rules for maintainable component and class structure.
- **[react-component-ownership](./skills/frameworks/react-component-ownership/SKILL.md)** — Apply ownership-boundary principles to React state, effects, queries, dialogs, tabs, forms, and component composition.

- [tailwind-discipline](skills/frameworks/css/tailwind-discipline/SKILL.md)
- [elysiajs](skills/frameworks/elysiajs/SKILL.md)
- [architecture](skills/frameworks/flutter/architecture/SKILL.md)
- [routing-discipline](skills/frameworks/go-router/routing-discipline/SKILL.md)
- [layout-system](skills/frameworks/layout-system/SKILL.md)
- [motion-discipline](skills/frameworks/motion/motion-discipline/SKILL.md)
- [app-router-discipline](skills/frameworks/next/app-router-discipline/SKILL.md)
- [component-discipline](skills/frameworks/react/component-discipline/SKILL.md)
- [form-discipline](skills/frameworks/react-hook-form/form-discipline/SKILL.md)
- [state-discipline](skills/frameworks/redux-toolkit/state-discipline/SKILL.md)
- [provider-discipline](skills/frameworks/riverpod/provider-discipline/SKILL.md)
- [shadcn-ui](skills/frameworks/shadcn-ui/SKILL.md)
- [app-discipline](skills/frameworks/tanstack-start/app-discipline/SKILL.md)
- [type-discipline](skills/frameworks/typescript/type-discipline/SKILL.md)
- [project-discipline](skills/frameworks/vite/project-discipline/SKILL.md)

### Personal

- **[anti-overengineering](./skills/personal/anti-overengineering/SKILL.md)** — Prefer simpler maintainable solutions over unnecessary abstractions and complexity.
- **[maintainability-first](./skills/personal/maintainability-first/SKILL.md)** — Prioritize readability, consistency, and long-term maintainability.
- **[startup-reality](./skills/personal/startup-reality/SKILL.md)** — Balance engineering quality with practical delivery constraints.
- **[db-philosophy](./skills/personal/db-philosophy/SKILL.md)** — Database philosophy focused on integrity and maintainable business-logic boundaries.
- **[human-debugging](./skills/personal/human-debugging/SKILL.md)** — Human-centered debugging focused on understanding systems and avoiding blame.

### Misc

- **[caveman](./skills/misc/caveman/SKILL.md)** — Keep engineering competent while narrating progress and results in compact caveman English.
