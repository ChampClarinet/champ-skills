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

## AI assistant behavior

When changing skills:

- keep `README.md` references in sync
- keep bucket `README.md` references in sync
- preserve YAML frontmatter in every `SKILL.md`
- prefer small logical commits
- use the git workflow skill when committing
