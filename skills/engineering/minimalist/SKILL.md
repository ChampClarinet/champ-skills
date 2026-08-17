---
name: minimalist
description: Minimal-diff implementation mode. Make the smallest correct change that satisfies the requested outcome; avoid adjacent refactors, speculative abstractions, and unrelated cleanup. Trigger on /minimalist or when the user explicitly asks for the smallest possible safe change.
---

# Minimalist

Small diff. Correct behavior. Nothing extra.

## Rules

- Identify the minimum behavior that must change.
- Prefer modifying existing code over introducing new abstractions when both are equally clear and correct.
- Do not refactor adjacent code merely because it could be cleaner.
- Do not add extensibility for hypothetical future requirements.
- Do not rename, reformat, reorganize, or upgrade unrelated code.
- Preserve existing public contracts unless the requested outcome requires changing them.
- Run the narrowest relevant verification that gives meaningful confidence.
- If a larger change is genuinely necessary for correctness, explain why before expanding scope when possible.

This complements scope-discipline: scope-discipline controls *what outcome* is allowed; minimalist controls *how much code* should move to achieve it.
