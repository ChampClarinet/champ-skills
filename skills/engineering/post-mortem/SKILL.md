---
name: post-mortem
description: Write the canonical engineering record of a validated bug fix: symptom, root-cause mechanism, fix, validation, escape path, and durable lessons. Use after debugging when the fix and cause are established, or when the user asks for an RCA or engineering write-up.
---

# Post-mortem

Record the engineering truth needed to understand the failure, recover the mental model, and avoid repeating the same class of bug.

Use `management-talk` separately when the same facts need a leadership-facing reframe.

## Preconditions

Do not present a hypothesis as a completed post-mortem.

Before writing a final post-mortem, require evidence for:

- the observed failure or strongest available failure signal
- the root-cause mechanism
- the implemented fix
- validation that the fix addresses the failure

A deterministic local reproducer is valuable but not mandatory. When one is unavailable, use the strongest production, integration, trace, log, or test evidence available and state the limitation explicitly.

If root cause, fix, or validation is still unresolved, use `debug-mantra` instead of manufacturing a completed RCA.

Trivial fixes do not require a post-mortem unless the user asks for one or the failure exposes a reusable lesson.

For a customer-visible incident or outage, do not pretend this bug-fix record replaces incident-specific timeline, impact, response, and communication artifacts.

## Required engineering record

Adapt the presentation to the destination, but preserve these facts.

### Summary

State what failed, the user or workload consequence, the root cause, and what fixed it.

### Symptom and evidence

Record what was actually observed: error, test failure, log, trace, workload behavior, performance signal, or customer report.

Distinguish direct evidence from inference.

### Root cause and mechanism

Explain the actual failure mechanism end to end.

Use concrete code identifiers, paths, conditions, state transitions, configuration, or commits when they materially help another engineer locate and understand the failure.

Connect the cause to the visible symptom. Do not stop at the first bad state if an earlier mechanism produced it.

### Fix

State what changed and why it addresses the root cause rather than merely suppressing the symptom.

Record relevant failed or partial prior fixes when they explain the mechanism or prevent the same mistake from recurring.

### Validation

State how the original failure signal, or the closest available equivalent, was checked after the fix.

Record regression coverage and the actual scope of validation. Do not imply configurations, workloads, browsers, devices, or environments were tested when they were not.

### Escape path

When useful, explain why existing tests, review, CI, monitoring, workload coverage, assumptions, or architecture allowed the bug through.

Describe the system gap, not a person to blame.

### Durable follow-up

Add follow-up work only when it prevents recurrence, closes an observed detection gap, or captures a durable architectural lesson.

Do not manufacture action items for ceremony. Include owner or tracking identifiers only when known or required by the destination.

## Debugging path

Include the debugging path only when it teaches something reusable or explains confidence in the diagnosis.

Useful details include:

- the evidence that narrowed the search
- important hypotheses that were falsified
- the experiment or observation that confirmed the mechanism
- misleading symptoms or failed fixes worth avoiding next time

Do not turn the post-mortem into a transcript of the debugging session or expose private chain-of-thought.

## Durable knowledge

Promote information beyond the post-mortem when the lesson has ongoing value.

Examples include:

- regression tests for the failure seam
- architecture or ownership rules
- CI or monitoring checks
- runbook or operational knowledge
- reusable debugging evidence
- a repository-local rule that should prevent the class of bug

The post-mortem records what happened. The appropriate permanent artifact should encode what the system should remember.

## Tone

Write for engineers.

Prefer mechanism over narrative, concrete identifiers over vague summaries, and evidence over confidence language.

Be blameless. State uncertainty and validation limits explicitly. Never invent root cause, ownership, links, validation, or follow-up work.

## Verification

Before treating the record as complete, confirm:

- root cause is established rather than merely suspected
- the cause-to-symptom chain is understandable
- the fix addresses the mechanism rather than only the symptom
- validation includes the original failure signal or closest available equivalent
- validation scope and uncertainty are stated honestly
- useful code identifiers remain searchable
- escape-path claims are evidence-based
- follow-ups exist only when they prevent a concrete recurrence or detection failure
- durable lessons are promoted when another artifact should own them

If any required fact is unsupported, mark it unresolved rather than filling the gap with plausible prose.
