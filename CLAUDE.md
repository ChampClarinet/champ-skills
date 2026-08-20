# Skill Repository Rules

Skills are organized into bucket folders under `skills/`:

- `engineering/` — debugging, review, RCA, git workflow, and engineering workflows
- `productivity/` — communication and workflow translation skills
- `frameworks/` — framework-specific conventions and architecture guidance
- `personal/` — personal engineering philosophies and decision-making heuristics
- `misc/` — rarely used or experimental utilities
- `in-progress/` — drafts not yet stable
- `deprecated/` — archived or no longer used

## Published skills

Skills in these folders are considered active and should appear in the top-level `README.md`:

- `engineering/`
- `productivity/`
- `frameworks/`
- `personal/`
- `misc/`

Each bucket folder should have a `README.md` listing every active skill in that bucket with a one-line description.

Each skill entry in the top-level `README.md` and bucket README must link the skill name to its `SKILL.md`.

## Draft / archived skills

Skills in these folders should not appear in the top-level `README.md` unless explicitly requested:

- `in-progress/`
- `deprecated/`

## Claude plugin metadata

`.claude-plugin/plugin.json` is Claude-specific metadata.

Only update `.claude-plugin/plugin.json` when explicitly working on Claude plugin packaging or Claude Code distribution.

Do not assume every active skill must be added to `.claude-plugin/plugin.json`.

## Scope discipline

When modifying code, configuration, documentation, or skills:

- make the smallest change necessary to satisfy the explicit request
- do not perform unrelated cleanup, refactoring, renaming, reformatting, modernization, or optimization
- treat discovered issues as out of scope unless they block the requested work
- finish the requested work first; offer worthwhile adjacent improvements afterward as optional follow-up work
- never implement optional follow-up work until the user explicitly opts in
- preserve existing behavior, APIs, dependencies, naming, and structure unless the requested outcome requires a change
- use the scope-discipline skill to govern what may change; task-specific skills govern how in-scope work is implemented

## Skill routing and composition

Skills may compose. Do not choose only one skill when multiple skills govern orthogonal parts of the task.

When implementing or refactoring code:

- always apply `scope-discipline` to determine what may change
- apply `ownership-boundaries` when the task involves decomposition, state ownership, side effects, data access, dependency direction, multiple cooperating units, or god-object/supercomponent risk
- when a framework-specific skill matches the technology being changed, apply it together with the relevant engineering skill rather than replacing it
- for React component architecture, apply `react-component-ownership` together with `ownership-boundaries`
- apply `tooling-feedback` when touched code has actionable compiler, type-checker, linter, language-server, editor, or framework-plugin diagnostics
- apply `file-structure` when creating or modifying project-owned React or Flutter UI code

Framework-specific skills translate general engineering principles into idiomatic implementation rules. General engineering skills remain responsible for their architectural or workflow concern.

## AI assistant behavior

When changing skills:

- keep `README.md` references in sync
- keep bucket `README.md` references in sync
- preserve YAML frontmatter in every `SKILL.md`
- prefer small logical commits
- use the git workflow skill when committing
