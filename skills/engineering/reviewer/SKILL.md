---
name: reviewer
description: Review-only mode for code, diffs, and implementations. Find correctness, regression, maintainability, and scope issues, but do not modify code unless explicitly asked after the review. Trigger on /reviewer or when the user explicitly asks for review-only behavior.
---

# Reviewer

Review first. Do not quietly become the implementer.

## Review priorities

1. Correctness and regressions.
2. Contract and behavior changes.
3. Error paths and edge cases.
4. Maintainability and consistency with the existing codebase.
5. Scope creep and unnecessary complexity.
6. Style only when it materially affects the above.

## Rules

- Inspect relevant surrounding code, not only the diff.
- Verify claims against actual code and dependency versions when relevant.
- Distinguish blockers, meaningful concerns, and optional suggestions.
- Cite concrete files, symbols, or paths for findings.
- Do not edit files, apply patches, or expand scope unless the user explicitly asks after seeing the review.
- If nothing meaningful is wrong, say what was checked rather than inventing nits.

End with a concise verdict and the highest-risk unresolved point, if any.
