---
name: git-workflow
description: Git workflow and commit discipline rules based on Champ's conventional-commit + gitmoji style, scoped commits, ticket handling, and Husky behavior.
---

# Git Workflow

Follow this workflow whenever creating commits, suggesting commit messages, splitting changes, or handling Git hooks.

## Core Rules

- Use Conventional Commit style.
- Prefix commit type with gitmoji.
- Prefer one task per commit.
- Break large work into logical commits.
- Avoid mixing unrelated changes in one commit.
- Keep commit history readable, reviewable, and easy to revert.
- Treat Git hooks as required validation, not an obstacle to work around.
- If a Git hook rejects a commit, diagnose and fix the underlying failure, then retry the commit normally.
- Never bypass hooks automatically with `--no-verify`, `HUSKY=0`, hook deletion, hook-path changes, or equivalent mechanisms.
- Hook bypass is allowed only when the user explicitly instructs bypassing the hook for that specific commit. Do not ask the user for permission to bypass as a fallback.

## Commit Format

Use this format:

```txt
<gitmoji> <type>(<scope>): <short imperative subject>
```

Scope is optional.

Examples:

```txt
✨ feat(skills): add git workflow skill
📝 docs(readme): update champ-skills overview
🐛 fix(flutter): correct ConsumerStatefulWidget state pairing
♻️ refactor(skills): simplify management-talk output flow
🚚 chore(config): update commitizen scopes
```

## Subject Rules

- Use short imperative tense.
- Keep subject under 100 characters.
- Be specific about the changed behavior or artifact.
- Do not end the subject with a period.

Good:

```txt
📝 docs(readme): add Codex usage notes
```

Bad:

```txt
📝 docs(readme): updated readme.
```

## Body Rules

Use a longer body when the subject alone is not enough.

Use the body to explain:

- why the change exists
- important tradeoffs
- migration notes
- context that reviewers need
- non-obvious implementation decisions

Keep it factual and concise.

## Footer / Ticket Rules

Tickets or task IDs are optional.

Only include them when explicitly provided by the user, task context, branch name, or repository workflow.

Examples:

```txt
Refs: TICKET-123
Closes: #31
Closes: #31, #34
```

Do not invent ticket numbers, issue IDs, or task references.

## Type Rules

Use only these commit types:

- `✨ feat` — adding a new feature
- `🐛 fix` — fixing a bug
- `📝 docs` — add or update documentation
- `💄 style` — add or update styles, UI, or UX
- `♻️ refactor` — code change that neither fixes a bug nor adds a feature
- `⚡️ perf` — code change that improves performance
- `✅ test` — adding or updating tests
- `🚚 chore` — build process, auxiliary tools, or documentation-generation changes
- `⏪️ revert` — revert a commit
- `🚧 wip` — work in progress
- `👷 build` — build process changes
- `💚 ci` — CI changes

## Scope Rules

Scopes are optional.

Prefer scopes when they improve readability or clarify the affected area.

Examples:

```txt
feat(auth): add refresh token support
fix(ui): correct mobile layout overflow
docs(readme): update installation guide
```

Custom scopes are encouraged when appropriate.

Avoid overly broad or meaningless scopes such as:

```txt
misc
stuff
update
fixes
```

## Breaking Changes

Breaking changes are allowed only for:

- `feat`
- `fix`

If a change is breaking, include a clear breaking-change note in the body or footer.

Example:

```txt
BREAKING CHANGE: rename auth token storage key from accessToken to authToken
```

## Task Breakdown

Before committing, group changes into logical tasks.

Prefer:

```txt
1 task = 1 commit
```

Examples:

- README rewrite → one docs commit
- add personal skill frontmatter → one docs/chore commit
- add file-structure skill → one feat/docs commit
- rename folders → one refactor/chore commit

Avoid:

- README rewrite + Flutter skill + Husky config + unrelated formatting in one commit

## Git Hook Rules

If Husky or any other Git hook rejects a commit:

1. Read the complete hook output and identify which validation failed.
2. Determine whether the failure comes from the staged changes, commit message, dependencies, configuration, or the hook/tooling itself.
3. Fix the underlying issue when it is within the task or repository scope.
4. Re-run the relevant validation directly when useful to confirm the fix.
5. Retry the commit normally with hooks enabled.
6. If the failure cannot be fixed safely or is outside the current task, stop and report the blocker instead of bypassing it.

Forbidden unless the user explicitly instructs bypassing the hook for that specific commit:

- `git commit --no-verify`
- `HUSKY=0 git commit ...`
- disabling or deleting hook files
- changing `core.hooksPath` to evade hooks
- editing hook configuration solely to make the commit pass without fixing the failure
- any equivalent mechanism that skips repository-required commit validation

Do not propose bypassing hooks, ask for permission to bypass them, or treat bypass as a normal fallback. A prior bypass instruction does not carry forward to later commits unless the user explicitly says it does.

## Suggested Commit Planning Output

When asked to commit or plan commits, respond with:

```txt
Commit plan:
1. <type(scope): subject>
   - files:
   - reason:

2. <type(scope): subject>
   - files:
   - reason:
```

Then wait for approval before running commits if the environment allows committing.

## Philosophy

Optimize for:

- readable project history
- easier review
- easier rollback
- cleaner changelogs
- clear task boundaries
- less surprise for future maintainers

## Type Selection Guidelines

Choose the commit type based on the intent of the change, not only the touched file type.

Examples:

- typo, comments, README, documentation updates
  → `📝 docs`

- cleanup, renaming, restructuring without behavior changes
  → `♻️ refactor`

- formatting, spacing, UI polish
  → `💄 style`

- behavior fixes
  → `🐛 fix`

- new capabilities
  → `✨ feat`
