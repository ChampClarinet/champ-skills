---
name: tooling-feedback
description: Treat compiler, type-checker, linter, language-server, framework-plugin, and editor diagnostics as actionable feedback on touched code. Trigger proactively when modifying code that produces warnings, deprecations, canonicalization suggestions, type diagnostics, lint findings, or framework/tooling recommendations; fix relevant warnings without turning the task into repository-wide cleanup.
---

# Tooling Feedback

Tooling feedback is part of implementation quality, not decoration.

Warnings from the active compiler, type checker, linter, language server, framework plugin, and editor integrations should be inspected when they affect code being changed.

## Core rule

> Leave touched code clean of actionable tooling warnings when they can be fixed safely without changing the requested behavior.

Do not ignore a warning merely because the code still compiles or runs.

## What to fix

Fix:

- warnings introduced by the current change
- existing warnings on lines or code paths materially modified by the task when the fix is local and behavior-preserving
- explicit deprecation replacements recommended by authoritative tooling
- canonical syntax or API replacements recommended by the framework or language tooling
- straightforward type or lint issues in the touched surface

Examples include:

- a Tailwind language-service canonical-class suggestion such as replacing `break-words` with `wrap-break-word`
- a TypeScript deprecation warning with a documented replacement
- a React lint warning caused by a changed dependency list
- a framework plugin warning about a touched API usage

## Scope boundary

Do not turn a local task into repository-wide warning cleanup.

If the same warning exists in unrelated files or untouched areas:

1. leave those areas unchanged by default
2. complete the requested task
3. optionally offer a separate cleanup if it is worthwhile

A warning outside the touched surface is not automatically in scope.

## Safety

Before applying a suggested fix, confirm that it is behavior-preserving or required for correctness.

Do not mechanically accept tooling suggestions when they:

- change runtime behavior unexpectedly
- alter public contracts
- require broad migrations
- conflict with repository conventions
- are known false positives
- depend on an uncertain tool or framework version

When the suggestion is ambiguous, verify against the active toolchain or framework documentation before changing behavior.

## Safe suppression fallback

If resolving a warning would change intended behavior, introduce meaningful regression risk, or require disproportionate refactoring, preserve the working behavior and suppress the diagnostic as narrowly as possible instead of forcing the suggested fix.

Prefer, in order:

1. fix the warning safely
2. use the tool or library's canonical supported alternative
3. suppress only the specific line, expression, or rule that cannot be fixed safely
4. disable a rule more broadly only when explicitly requested or when the repository already documents that policy

When suppressing a diagnostic:

- use the smallest supported scope, preferably the next line or exact expression
- name the exact rule or diagnostic identifier when the tool supports it
- add a short reason when the intent is not obvious
- preserve behavior intentionally; do not use suppression to avoid a safe straightforward fix
- never disable an entire linter, checker, plugin, or ruleset just to silence one local warning

For example, when a React hook dependency warning is intentionally not fixable without changing the effect's required lifecycle, prefer a targeted suppression such as:

```ts
// eslint-disable-next-line react-hooks/exhaustive-deps -- intentional: effect must only run on mount
```

Do not convert a local exception into project-wide configuration churn.

## Validation

After fixing or suppressing a warning:

- re-run or re-check the narrowest relevant diagnostic source when practical
- ensure the warning is gone or intentionally suppressed at the narrowest scope
- ensure no new warning was introduced nearby
- preserve the requested behavior

## Interaction with other skills

- `scope-discipline` limits cleanup to the requested and touched surface.
- `minimalist` favors the smallest safe warning fix or suppression.
- framework-specific skills decide the idiomatic replacement when tooling feedback is framework-specific.

Tooling feedback should improve touched code without silently expanding the task.
