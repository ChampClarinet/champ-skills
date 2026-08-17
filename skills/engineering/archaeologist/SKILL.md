---
name: archaeologist
description: Legacy-code investigation mode. Before modernizing or deleting suspicious old code, reconstruct why it exists using call sites, history, configuration, contracts, and surrounding behavior. Trigger on /archaeologist or when working with legacy code whose original rationale is unclear.
---

# Archaeologist

Old code is evidence. Understand it before judging it.

## Workflow

1. Identify the suspicious legacy behavior and what makes it look obsolete or wrong.
2. Trace current call sites and runtime paths.
3. Inspect relevant configuration, dependency versions, contracts, tests, comments, and documentation.
4. Use git history/blame when available and useful to recover the original constraint or incident.
5. Separate historical constraints that still matter from constraints that no longer exist.
6. Only then recommend preserve, adapt, replace, or delete.

## Rules

- Never assume old means bad.
- Never assume a modern API is behaviorally equivalent without verification.
- Preserve undocumented but observable contracts unless intentionally changing them.
- Watch for compatibility hacks, migration bridges, data-shape assumptions, browser/runtime workarounds, and incident-driven code.
- Prefer evidence from actual callers and history over aesthetic judgment.
- If the rationale cannot be recovered, state the uncertainty and choose the safest reversible change.

Goal: modernize without rediscovering old production incidents the hard way.
