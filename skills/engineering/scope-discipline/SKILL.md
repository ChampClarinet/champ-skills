---
name: scope-discipline
description: Keep AI-assisted implementation tightly bounded to the user's requested outcome. Complete the requested scope first, then optionally suggest worthwhile adjacent improvements and wait for approval before doing them. Trigger proactively whenever modifying code, configuration, documentation, or repository files.
---

# Scope Discipline

Keep implementation bounded to the user's request. The default is the smallest change that fully satisfies the requested outcome.

Do not silently broaden the task just because nearby code could also be improved. Finish the requested work first. If you notice a worthwhile adjacent improvement, offer it afterward as an optional follow-up and wait for the user to opt in before changing anything else.

## Core rule

> Do the brief first. Upsell improvements afterward.

The user's explicit request is the implementation scope boundary.

A discovered problem is not automatically part of the task.

"While I'm here" is not a valid reason to modify code.

A good extra idea is something to offer, not something to silently include.

## Before editing

Identify three things:

1. **Requested outcome** — what observable result did the user ask for?
2. **Required surface** — which files, behaviors, APIs, or configuration must change to produce that result?
3. **Optional opportunities** — useful adjacent improvements that are not required by the brief.

Only the first two belong in the current implementation by default.

When the request is ambiguous in a way that materially changes what the requested outcome itself means, ask before proceeding. Do not use clarification as a reason to interrupt for optional improvements.

## During editing

For every proposed modification, ask:

> Is this change necessary to achieve the requested outcome?

If yes, it is in scope.

If no, do not make it now. Record it as an optional follow-up if it is worth mentioning.

Do not silently perform unrelated:

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

## Optional follow-ups: the upsell rule

After the requested work is complete, you may suggest worthwhile adjacent improvements.

Keep the offer concise and actionable. Explain:

1. what the extra change would be,
2. why it may be useful,
3. the main tradeoff or extra scope if non-obvious.

Then ask whether the user wants it.

Examples:

- "Done. I also noticed the duplicated validation can be collapsed into the existing helper, which would touch two extra files. Want me to clean that up too?"
- "The requested fix is complete. There is also an outdated dependency in this path, but it is unrelated to the bug. Want me to check the upgrade separately?"
- "This works within the existing API. A broader refactor could simplify the flow, but it would expand the patch. Want to debate that option before changing it?"

Do not make the optional change unless the user explicitly opts in.

If the user declines or ignores the offer, the completed brief remains complete. Do not keep pushing the suggestion.

## Adjacent problems

If you discover an unrelated bug, smell, security concern, outdated pattern, or maintainability issue:

1. Determine whether it blocks the requested task.
2. If it does not block the task, leave it unchanged.
3. Finish the requested work.
4. Mention it afterward only if it is useful enough to justify the user's attention.
5. Ask whether the user wants a separate follow-up change.

If an adjacent issue genuinely blocks the requested outcome, it is not an optional upsell. Make only the minimum supporting change required to complete the brief and explain why it was necessary.

For serious security, data-loss, or correctness risks, surface the finding clearly. Still avoid unrelated broad remediation without approval when the requested task can be completed safely without it.

## Refactoring

A refactor is automatically in scope only when:

- the user explicitly requested the refactor, or
- the requested behavior cannot be implemented safely without a narrow supporting refactor.

Do not refactor merely because the current code is awkward, duplicated, old, inconsistent, or different from your preferred architecture.

If a broader refactor would be valuable but is not required, finish the narrow implementation first and offer the refactor afterward.

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

Optional improvements belong in the final follow-up offer, not in the diff.

## Interaction with other skills

This skill governs **what may change**. Other engineering or framework skills govern **how an in-scope change should be implemented**.

When another skill identifies an improvement outside the user's requested outcome, complete the requested work first and offer the extra improvement afterward.

Examples:

- `debug-mantra` may discover multiple defects; fix the requested defect, then offer unrelated fixes separately unless another defect blocks it.
- `scrutinize` may identify additional review findings; keep them out of the current patch and offer them as follow-up work.
- framework conventions should guide touched code, not trigger repository-wide migrations; offer a migration separately if useful.
- `git-workflow` should commit only the requested scope and necessary supporting changes.

## Completion test

Before declaring the task complete, be able to answer yes to all of these:

- Does the result satisfy the explicit request?
- Is every changed behavior necessary for that result?
- Did unrelated behavior remain unchanged?
- Did I avoid opportunistic cleanup and refactoring?
- Are optional improvements kept out of the diff until the user opts in?
- Can every meaningful diff hunk be traced back to the requested outcome or a necessary supporting change?
