# Skill Repository Rules

Skills are organized into bucket folders under `skills/`:

- `engineering/` — debugging, review, RCA, git workflow, orchestration, and engineering workflows
- `productivity/` — communication and workflow translation skills
- `frameworks/` — framework-specific conventions and architecture guidance
- `personal/` — personal engineering philosophies and decision-making heuristics
- `misc/` — rarely used or experimental utilities
- `in-progress/` — drafts not yet stable
- `deprecated/` — archived or no longer used

## Published skills

Skills in active buckets must appear in the top-level and bucket README with a link to their `SKILL.md`. Draft and deprecated skills stay out unless explicitly requested.

Every published `SKILL.md` must preserve YAML frontmatter. Follow [docs/skill-authoring.md](docs/skill-authoring.md) when authoring or refactoring skills.

## Claude plugin metadata

`.claude-plugin/plugin.json` is Claude-specific. Update it only when explicitly working on Claude plugin packaging or distribution.

## Scope discipline

When modifying code, configuration, documentation, or skills, apply `scope-discipline`: make the smallest change that satisfies the explicit request and keep optional adjacent work out of the diff until the user opts in.

## Skill routing and composition

Use `skill-router` as the shared composition policy for non-trivial engineering work.

Normal platform skill discovery identifies relevant skills. The router then resolves authority, required companions, optional overlays, and execution hints. Do not load every vaguely related skill.

Authority is:

1. platform/system constraints
2. explicit user instructions
3. repository-local instructions and skills
4. champ-skills hard policies
5. champ-skills guidance
6. framework defaults and model judgment

Repository-local explicit rules override champ-skills personal defaults. Ambiguous repository patterns are not automatic overrides.

General engineering skills own cross-framework concerns. Framework skills translate those concerns only where framework mechanics matter.

For repository modifications, `scope-discipline` governs what may change. Use `ownership-boundaries` when behavioral ownership is materially involved, `file-structure` when physical component/file boundaries change, and `tooling-feedback` for actionable diagnostics on touched code.

Use `agent-orchestration` when delegation could materially improve execution. Delegation is based on expected benefit versus coordination cost, not fixed roles or agent counts.

## AI assistant behavior

When changing skills:

- keep top-level and bucket README references in sync
- preserve YAML frontmatter in every published `SKILL.md`
- prefer small logical commits
- use `git-workflow` when committing
- do not duplicate canonical rules across framework adapters
- do not add mandatory ceremony without a concrete failure mode it prevents
