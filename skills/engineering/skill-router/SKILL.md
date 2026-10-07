---
name: skill-router
description: Compose champ-skills for non-trivial engineering work by resolving authority, required companion skills, optional overlays, and execution hints without loading unrelated skills.
---

# Skill Router

Compose relevant skills after normal skill discovery. Do not replace discovery with a giant task-to-skill catalogue.

## Authority

Resolve conflicts in this order:

1. platform or system constraints
2. explicit user instructions
3. repository-local instructions and skills
4. champ-skills hard policies
5. champ-skills guidance
6. framework defaults and model judgment

Repository-local explicit policy overrides champ-skills because the active repository owns its conventions. Do not treat an ambiguous or merely existing repository pattern as an explicit override.

When two instructions at the same authority level materially conflict and neither can safely satisfy both, surface the conflict, consequences, and options to the user rather than silently choosing.

## Composition

Load the minimum useful skill set.

For repository modifications, apply `scope-discipline` to govern what may change.

Add canonical engineering skills when their concern is materially involved. Framework skills adapt those principles to framework mechanics; they do not replace or duplicate the canonical owner.

Add optional stance or philosophy skills only when they improve the task. Do not activate a skill merely because a weak keyword match exists.

Prefer one canonical owner for each concern:

- scope: `scope-discipline`
- behavioral ownership: `ownership-boundaries`
- physical component/file policy: `file-structure`
- debugging evidence discipline: `debug-mantra`
- execution topology and delegation: `agent-orchestration`
- actionable touched-surface diagnostics: `tooling-feedback`
- Git/commit discipline: `git-workflow`

## Conflict handling

When active skills appear to disagree:

1. Resolve by authority when possible.
2. A hard invariant beats guidance at the same authority level.
3. If both can be satisfied, compose them.
4. For a low-impact ambiguity, choose the smallest reversible interpretation.
5. For a meaningful unresolved decision, ask the user.

Do not let a framework adapter silently override a repository rule or a champ hard policy.

## Execution topology

Domain skills may identify separable, parallelizable, or independently verifiable work. They do not prescribe agent counts or fixed roles.

Use `agent-orchestration` when delegation could materially improve parallelism, context isolation, independent verification, or model/cost efficiency. Keep cohesive work single-core when coordination cost would dominate.

## Verification

Before finishing non-trivial work, verify that:

- active skills cover the actual concerns and no irrelevant skill drove scope
- repository-local rules won over conflicting personal defaults
- each concern has one canonical policy owner
- optional guidance did not override hard constraints
- unresolved meaningful conflicts were surfaced to the user
- delegation, if used, earned its coordination cost
