---
name: verification
description: Select sufficient evidence for acceptance criteria and report actual verification coverage. Apply to implementation changes; distinguish static checks, behavioral tests, runtime evidence, and unverified outcomes.
---

# Verification

Passing checks does not imply passing acceptance criteria.

## Hard policies

- Identify the observable acceptance criteria and material regression risks before selecting checks.
- Use the cheapest sufficient evidence, not merely the cheapest available check. Broaden verification when narrower evidence cannot support the claim.
- Never substitute lint, typecheck, build success, or mocked behavior for evidence of actual behavior when that behavior is material to acceptance.
- Preserve test integrity. Do not weaken assertions, mock away the relevant failure path, skip failing checks, or change expected results merely to obtain green tests. Change expectations only when justified by the intended contract.
- Distinguish passed, failed, and unverified criteria. Never claim a fix or feature is verified when required evidence is missing.

## Select evidence

Choose checks according to the claim and risk, not a mandatory test pyramid:

- Static inspection and tooling for source-level properties.
- Unit tests for isolated logic.
- Contract or integration checks for boundaries, serialization, persistence, and interactions.
- Targeted runtime or end-to-end checks when actual execution or user behavior is material.
- Relevant regression checks for affected existing behavior.

Use existing project tooling and repository-required checks. Add or update automated tests when needed for sufficient evidence or durable regression protection. Do not mandate new infrastructure, exhaustive suites, or artifacts for every task.

## Completion

Inspect actual results, including failures. Report what was checked, the result, and material limitations. If required verification is unavailable, use the strongest available alternative without claiming equivalent coverage. Report implementation separately from verification; mark affected criteria unverified and identify the remaining check. Do not declare full completion while required criteria remain unresolved.

## Composition

This skill owns general acceptance evidence and verification sufficiency. Scope-discipline owns the allowed change surface; debug-mantra owns failure diagnosis; visual-verification owns rendered evidence; tooling-feedback owns diagnostics; agent-orchestration owns independent verification and escalation. Review modes remain optional according to intent and risk.
