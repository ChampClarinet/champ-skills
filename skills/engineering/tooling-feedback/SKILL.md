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

## Validation

After fixing a warning:

- re-run or re-check the narrowest relevant diagnostic source when practical
- ensure the warning is gone
- ensure no new warning was introduced nearby
- preserve the requested behavior

## Interaction with other skills

- `scope-discipline` limits cleanup to the requested and touched surface.
- `minimalist` favors the smallest safe warning fix.
- framework-specific skills decide the idiomatic replacement when tooling feedback is framework-specific.

Tooling feedback should improve touched code without silently expanding the task.
