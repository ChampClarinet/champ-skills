---
name: tooling-feedback
description: Treat compiler, type-checker, linter, language-server, framework-plugin, and editor diagnostics as actionable feedback on touched code. Use when modified code produces warnings, deprecations, canonicalization suggestions, type diagnostics, lint findings, or framework/tooling recommendations.
---

# Tooling Feedback

Leave touched code clean of actionable tooling diagnostics when they can be resolved safely without changing the requested behavior.

A warning is evidence to inspect, not an instruction to obey mechanically.

## In-scope diagnostics

Address:

- diagnostics introduced by the current change
- existing diagnostics on materially modified code when the correction is local and behavior-preserving
- authoritative deprecation replacements
- canonical syntax or API replacements recommended by the active language or framework tooling
- straightforward type or lint findings on the touched surface

Do not turn a local task into repository-wide warning cleanup. Unrelated diagnostics remain outside scope unless the user opts into broader cleanup.

Compose with `scope-discipline` for the exact change boundary.

## Evaluate before applying

Before accepting a tooling suggestion, determine whether it is valid for the repository's active toolchain and preserves intended behavior.

Do not mechanically apply suggestions that:

- change runtime behavior or public contracts
- require broad migration
- conflict with explicit repository conventions
- are false positives
- depend on an uncertain tool or framework version

When validity depends on version or framework behavior, verify against the active toolchain or authoritative documentation.

Framework-specific skills determine the idiomatic replacement when relevant.

## Resolution order

Prefer, in order:

1. fix the diagnostic safely
2. use the tool or library's canonical supported alternative
3. narrowly suppress the specific diagnostic when fixing it would change intended behavior, create meaningful regression risk, or require disproportionate refactoring
4. broaden suppression only when explicitly requested or already established by repository policy

Suppression is an intentional exception, not cleanup.

When suppressing:

- use the smallest supported scope
- name the exact rule or diagnostic when supported
- state the reason when intent is not obvious
- preserve the intended behavior
- never disable an entire checker, linter, plugin, or ruleset merely to silence one local warning

Do not convert a local exception into project-wide configuration churn.

## Verification

After resolving or suppressing an in-scope diagnostic:

- re-run or re-check the narrowest relevant diagnostic source when practical
- confirm the original diagnostic is gone or intentionally suppressed
- check that the correction did not introduce nearby diagnostics
- preserve the requested behavior
- keep unrelated repository diagnostics outside the patch

Tooling feedback improves the touched surface; it does not expand the task.
