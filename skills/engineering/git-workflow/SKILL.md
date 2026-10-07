---
name: git-workflow
description: Champ's Git Flow, branch naming, gitmoji Conventional Commit, scoped-commit, and hook-validation policy. Use when creating branches or commits, planning Git history, or handling Git hooks.
---

# Git Workflow

Repository-local explicit Git policy overrides these defaults. Otherwise use standard Git Flow with the branch and commit rules below.

## Hard invariants

- Every commit message starts with the appropriate gitmoji.
- Use Conventional Commit semantics after the gitmoji.
- Keep commits logically scoped and independently reviewable/revertible.
- Never bypass repository Git hooks unless the user explicitly instructs bypassing them for that specific commit.
- Do not invent ticket or issue identifiers.

## Branch model

When the repository does not explicitly require another branch model:

- `main` — main production branch
- `develop` — main development/integration branch
- `feature/*` — feature or planned enhancement branches
- `fix/*` — normal bug or issue fix branches
- `hotfix/*` — urgent production fix branches

Follow standard Git Flow semantics for the rest of the lifecycle.

Normal feature and fix work branches from `develop`. Urgent production hotfixes branch from `main`.

Completed feature and fix work integrates through `develop`. Release and hotfix integration follows standard Git Flow unless repository-local policy says otherwise.

Use short lowercase kebab-case suffixes when practical:

```text
feature/pet-sharing
feature/skill-v2
fix/account-overflow
hotfix/oauth-callback
```

Do not invent personal prefixes such as refactor/_ or chore/_ when the repository has not defined them.
Classify planned non-emergency work under feature/_. Classify defect or issue correction under fix/_.
Commit format
Use:

```text
<gitmoji> <type>(<scope>): <short imperative subject>
```

The gitmoji prefix is mandatory. Scope is optional.
Examples:

```text
✨ feat(skills): add skill composition router
🐛 fix(ui): correct mobile layout overflow
📝 docs(readme): update installation guide
♻️ refactor(skills): simplify ownership rules
🚚 chore(config): update commitizen scopes
```

Use short imperative subjects, normally under 100 characters, with no trailing period.

## Commit types

Use:

- `✨ feat` — new capability
- `🐛 fix` — bug fix
- `📝 docs` — documentation
- `💄 style` — styling/UI/UX-only change
- `♻️ refactor` — restructuring without feature/fix behavior
- `⚡️ perf` — performance improvement
- `✅ test` — tests
- `🚚 chore` — auxiliary/config/tooling maintenance
- `⏪️ revert` — revert
- `🚧 wip` — explicitly intended work in progress
- `👷 build` — build-system change
- `💚 ci` — CI change

Choose the commit type from the intent of the change, not merely the type of file touched.
Breaking changes are allowed only for `feat` or `fix` and must state the breaking change clearly.

## Commit boundaries

Prefer one logical task per commit.
Split unrelated changes even when they happen during the same working session.
Use a commit body when reviewers need the reason, tradeoff, migration detail, or other non-obvious context.
Ticket and issue references are optional. Include them only when supplied by the user, task context, branch name, or repository workflow.
Do not invent ticket numbers or issue IDs.

## Git hooks

Treat Git hooks as required validation, not obstacles to work around.
If a hook fails:

1. Read the complete failure.
2. Identify whether staged changes, the commit message, dependencies, configuration, or tooling caused it.
3. Fix the underlying in-scope problem.
4. Re-run relevant validation when useful.
5. Retry normally with hooks enabled.

If the failure cannot be fixed safely within scope, report the blocker.
Do not use `--no-verify`, `HUSKY=0`, hook deletion, `core.hooksPath` changes, or equivalent bypasses unless the user explicitly requested bypass for that specific commit.
Do not offer hook bypass as the normal fallback. A bypass instruction for one commit does not carry forward to later commits.

## Verification

Before publishing Git work, confirm:

- branch name and base follow repository policy or the default Git Flow above
- every new commit starts with the appropriate gitmoji
- commit messages use the intended Conventional Commit type
- commits do not mix unrelated tasks
- required hooks and validation passed without hidden bypass
- release and hotfix integration preserves the repository's Git Flow
