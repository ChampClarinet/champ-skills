---
name: show-me
description: Explain complex requirements, plans, code structure, flows, and changes with the smallest effective visual representation; use when visuals materially improve understanding or the user explicitly requests them.
---

# Show Me

Skip unnecessary preamble. Keep prose brief and choose the smallest view that makes the key point clear. Use one or several representations only as needed.

- Interpret screenshots, sketches, and annotations alongside textual requirements. Distinguish visible facts from inferred intent; clarify consequential ambiguity.
- Use pseudocode for algorithms, call trees for runtime control flow, component trees for UI ownership and state boundaries, and shallow annotated file trees for module responsibilities.
- Use Mermaid for interactions, state transitions, and data flow when supported; otherwise use plain text.
- Use shape-aware diffs for changes to existing component trees, file layouts, call trees, or control flow. Show the whole block when most is new, omitted context hides ownership or order, or a copyable target is needed.
- Ground explanations of existing code in inspected source and relevant file paths or symbols. Label proposed shapes and illustrative examples as such.
- For UI layouts, state comparisons, or concepts too dense for simpler views, create one focused HTML artifact when useful and supported. Match existing product tokens and components, use grounded labels and data, and support desktop and mobile. Open or expose it through an available platform-appropriate mechanism; report limitations rather than claiming it was opened.
- Place each visual next to the short text it supports. Omit irrelevant calls, files, props, and states, but retain consequential failure paths and boundaries.

Distinguish observed, proposed, and verified states. A mockup or diagram is not runtime evidence; do not claim verification without actual execution evidence.

Do not expand implementation scope, replace the primary workflow, or create redundant artifacts. Plain prose is preferable when it communicates equally well at lower cost.

## Examples

```text
submitForm
  validateInput
  createSession
    persistPrompt
    launchAgent
  navigateToSession
```

```diff
 <SessionPage>
   <SessionToolbar>
+    <RunSkillButton />
   <SessionTimeline>
+    <SkillResultCard />
```

Adapted from the Show Me skill supplied by the user; upstream reference: https://github.com/humanlayer/skills (exact source path not verified).
