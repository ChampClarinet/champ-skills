---
name: debug-mantra
description: Evidence-driven debugging discipline. Use when diagnosing incorrect, failing, flaky, or unexplained system behavior.
---

# Debug Discipline

Diagnose from evidence before changing code.

## Core invariants

- Establish the strongest practical failure signal or evidence available.
- Trace the actual failure path before proposing a fix.
- Treat root-cause ideas as hypotheses, not conclusions.
- Seek evidence that could disprove the leading hypothesis.
- Reconcile new observations with previous evidence.
- Fix the root cause rather than merely hiding the symptom.
- Verify the original failure signal after the fix.
- Run relevant regression checks.

## Decision rules

Prefer a deterministic reproduction when practical.

If reproduction is flaky, improve its signal when the expected debugging value justifies the effort.

If local reproduction is unavailable, continue from the strongest available evidence such as logs, traces, captured artifacts, production telemetry, tests, or static execution paths. State uncertainty explicitly rather than pretending the issue was reproduced.

Choose debugging techniques according to the failure: debugger, source tracing, configuration comparison, instrumentation, stress/repetition, history, or other relevant tools. No single technique is mandatory for every bug.

Maintain an experiment ledger when multiple runs or hypotheses would otherwise lose useful evidence. A ledger records what changed, what happened, and what the observation ruled in or out; it is not a transcript.

## Before fixing

A proposed root cause should explain the observed failure end-to-end.

Before committing to it, ask what observation would contradict it and test that when practical. Generate alternatives when evidence supports more than one plausible mechanism; do not invent an arbitrary number merely to satisfy a ritual.

If existing evidence contradicts the hypothesis, refine or reject it before fixing.

## Verification

After the fix:

1. re-run the original failure signal or closest available equivalent
2. verify the mechanism no longer fails for the expected reason
3. run relevant regression checks
4. state material uncertainty or unverified coverage

Do not declare success solely because a new test is green while the original failure path remains unverified.
