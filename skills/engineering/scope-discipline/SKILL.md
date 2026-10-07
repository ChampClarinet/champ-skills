---
name: scope-discipline
description: Keep AI-assisted implementation bounded to the user's requested outcome. Apply proactively whenever modifying code, configuration, documentation, or repository files; complete required scope first and offer adjacent improvements separately.
---

# Scope Discipline

Do the brief first. Upsell improvements afterward.

The user's requested outcome defines what may change. A discovered problem is not automatically part of the task.

## Scope boundary

Before editing, identify:

1. **Requested outcome** — the observable result the user asked for.
2. **Required surface** — behavior, files, APIs, configuration, and validation that must change to produce it.
3. **Optional opportunities** — adjacent improvements that are useful but unnecessary for the requested outcome.

Only the first two are in scope by default.

If ambiguity materially changes the requested outcome, ask. Do not interrupt merely to clarify optional improvements.

For every proposed modification, ask:

> Is this necessary to achieve or validate the requested outcome safely?

If not, leave it out of the current patch.

## In-scope supporting work

A supporting change is in scope when the requested outcome cannot be implemented or validated safely without it.

Examples include:

- a narrow refactor required to implement the behavior safely
- tests needed to prove the requested behavior or prevent its regression
- a blocking defect discovered on the required execution path
- configuration or API adjustment required by the requested behavior

Keep supporting work as narrow as possible. Do not let it cascade into unrelated cleanup.

Validation is part of the requested change. Run the narrowest relevant checks first and broaden only when the change surface or repository workflow requires it.

## Out-of-scope work

Do not silently perform unrelated:

- cleanup or reformatting
- refactoring or renaming
- modernization or optimization
- dependency upgrades
- API redesign
- file or folder reorganization
- abstraction for hypothetical future requirements

Prefer existing patterns and APIs when they can satisfy the brief cleanly.

Do not change naming, formatting, dependencies, configuration, public APIs, or file structure merely because the touched area could be improved.

## Adjacent findings

If an adjacent issue does not block the requested outcome, leave it unchanged.

Mention it afterward only when it is useful enough to justify the user's attention. State the improvement and material tradeoff or extra scope, then wait for opt-in before changing it.

Do not repeatedly push a declined or ignored follow-up.

For serious security, data-loss, or correctness risks, surface the finding clearly even when it is outside scope. Do not silently broaden remediation when the requested work can still be completed safely without it.

## Refactoring

Refactoring is automatically in scope only when:

- the user explicitly requested it, or
- a narrow supporting refactor is required for safe implementation or validation.

Awkward, duplicated, old, inconsistent, or non-preferred code is not sufficient reason by itself.

A broader worthwhile refactor is a separate follow-up.

## Composition

This skill owns **what may change**.

Other skills determine how an in-scope change should be implemented:

- `ownership-boundaries` decides who should own behavior
- `file-structure` decides where owned units live
- framework skills map the change to framework mechanics
- `debug-mantra` may discover other defects, but unrelated defects remain separate unless blocking
- `scrutinize` may report adjacent findings without adding them to the patch
- `tooling-feedback` cleans actionable diagnostics on the touched surface without starting repository-wide cleanup
- `git-workflow` records only the requested scope and necessary supporting work

## Verification

Before completion, review the final diff against the requested outcome.

Every meaningful changed behavior and diff hunk must trace to:

- the requested outcome
- a necessary supporting change
- required validation

Remove changes justified only by convenience, aesthetics, speculative improvement, unrelated formatting, unnecessary renaming, or opportunistic cleanup.

Optional improvements belong outside the diff until the user opts in.
