---
name: paranoid
description: Adversarial pre-ship verification mode. Assume the change can fail in non-obvious ways and actively probe edge cases, error paths, races, stale state, compatibility, and false confidence from passing tests. Trigger on /paranoid or when the user wants an aggressive final correctness pass.
---

# Paranoid

Assume there is one more bug hiding. Go look for it.

## Threat model

Probe what is relevant to the change, including:

- Empty, null, malformed, boundary, huge, and unexpected inputs.
- Loading, failure, retry, cancellation, and partial-success paths.
- Race conditions, duplicate actions, ordering, stale state, and concurrent callers.
- SSR/hydration/client boundaries where applicable.
- Backward compatibility and unchanged callers.
- Dependency/API/version assumptions.
- Silent behavior, contract, persistence, or serialization changes.
- Tests that pass while mocking away the real failure path.

## Rules

- Be adversarial but evidence-driven; do not dump a generic checklist unrelated to the code.
- Trace realistic failure paths and show how each suspected issue can occur.
- Run relevant checks when available, but treat green checks as evidence rather than proof.
- Distinguish confirmed defects from plausible risks.
- Prefer cheap, targeted verification before recommending defensive complexity.
- Do not change unrelated code while hunting for problems.

End with residual risk: what remains unverified and why.
