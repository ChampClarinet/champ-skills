---
name: scope-discipline
description: Keep AI-assisted implementation tightly bounded to the user's requested outcome. Make the smallest sufficient change, preserve unrelated behavior and structure, and report adjacent issues instead of fixing them without approval. Trigger proactively whenever modifying code, configuration, documentation, or repository files.
---

# Scope Discipline

Keep implementation bounded to the user's request. The goal is the smallest change that fully satisfies the requested outcome, not the largest set of improvements that can be justified while touching the code.

## Core rule

> Make the smallest change that fully satisfies the user's request.

The user's explicit request is the scope boundary. Do not broaden it merely because adjacent code could be improved.

A discovered problem is not automatically part of the task.

"While I'm here" is not a valid reason to modify code.

## Before editing

Identify three things:

1. **Requested outcome** — what observable result did the user ask for?
2. **Required surface** — which files, behaviors, APIs, or configuration must change to produce that result?
3. **Out of scope** — what nearby code can remain untouched while the requested outcome still works?

If a change is not necessary for the requested outcome, leave it alone.

When the request is ambiguous in a way that materially changes scope, ask rather than silently choosing the broader interpretation.

## During editing

For every proposed modification, ask:

> Is this change necessary to achieve the requested outcome?

If the answer is no, do not make it.

Do not perform unrelated:

- cleanup
- refactoring
- renaming
- reformatting
- modernization
- optimization
- dependency upgrades
- API redesign
- file or folder reorganization
- abstraction for hypothetical future requirements

Prefer:

- local changes over cross-cutting refactors
- existing patterns over introducing new patterns
- preserving existing APIs over redesigning them
- preserving existing behavior over opportunistic correction
- the fewest touched files that cleanly solve the task

Do not change naming, formatting, dependencies, configuration, public APIs, or file structure unless the requested outcome requires it.

## Adjacent problems

If you discover an unrelated bug, smell, security concern, outdated pattern, or maintainability issue:

1. Do not silently fix it.
2. Determine whether it blocks the requested task.
3. If it does not block the task, leave it unchanged.
4. Mention it separately when it is useful for the user to know.
5. Ask for approval before expanding the implementation scope.

If it genuinely blocks the requested outcome, make only the minimum supporting change needed and explain why that supporting change was necessary.

## Refactoring

A refactor is in scope only when:

- the user explicitly requested the refactor, or
- the requested behavior cannot be implemented safely without it.

Do not refactor merely because the current code is awkward, duplicated, old, inconsistent, or different from your preferred architecture.

When a supporting refactor is unavoidable, keep it as narrow as possible and avoid cascading cleanup.

## Tests and validation

Validation is part of the requested change; unrelated product changes are not.

Add or update tests when they are necessary to prove the requested behavior or prevent regression. Do not use test work as a reason to redesign unrelated production code.

Run the narrowest relevant checks first. Broaden validation only when the change surface or repository workflow requires it.

## Before finishing

Review the final diff against the original request.

Remove any change that exists only because it was:

- convenient
- aesthetically preferable
- an opportunistic cleanup
- a speculative improvement
- unrelated formatting churn
- an unnecessary rename
- an unnecessary abstraction

Every changed file and meaningful diff hunk should be explainable by the user's request or by a necessary validation/supporting change.

## Interaction with other skills

This skill governs **what may change**. Other engineering or framework skills govern **how an in-scope change should be implemented**.

When another skill suggests an improvement outside the user's requested outcome, this scope discipline wins: report the improvement instead of implementing it.

Examples:

- `debug-mantra` may discover multiple defects; fix only the defect in the requested debugging scope unless another defect blocks it.
- `scrutinize` may identify unrelated review findings; report them separately instead of silently expanding the patch.
- framework conventions should guide touched code, not trigger repository-wide migrations.
- `git-workflow` should commit only the changes that survived this scope review.

## Completion test

Before declaring the task complete, be able to answer yes to all of these:

- Does the result satisfy the explicit request?
- Is every changed behavior necessary for that result?
- Did unrelated behavior remain unchanged?
- Did I avoid opportunistic cleanup and refactoring?
- Are adjacent findings reported rather than silently fixed?
- Can every meaningful diff hunk be traced back to the requested outcome?
