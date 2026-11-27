---
name: minimalist
description: Minimal-diff implementation mode. Make the smallest correct and maintainable change that satisfies the requested outcome; avoid adjacent refactors, speculative abstractions, and unrelated cleanup. Trigger on /minimalist or when the user explicitly asks for the smallest possible safe change.
---

# Minimalist

Small diff when equally correct and maintainable. Correct behavior. Nothing extra.

## Rules

- Identify the minimum behavior that must change.
- Prefer modifying existing code over introducing new abstractions when both are equally clear and correct.
- Do not refactor adjacent code merely because it could be cleaner.
- Do not add extensibility for hypothetical future requirements.
- Do not rename, reformat, reorganize, or upgrade unrelated code.
- Preserve existing public contracts unless the requested outcome requires changing them.
- Run the narrowest relevant verification that gives meaningful confidence.
- If a larger in-scope change is justified by correctness or concrete maintainability concerns, explain why. Do not preserve a defective structure merely to minimize the diff. Ask before expanding the approved scope.

This complements scope-discipline: scope-discipline controls *what outcome* is allowed; minimalist prefers less code movement among equally correct and maintainable solutions. Scope-discipline remains authoritative for structural freedom and justified refactoring.
