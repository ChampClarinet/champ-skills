---
name: agent-orchestration
description: Choose and coordinate single-agent or multi-agent execution for substantial engineering work. Use when delegation, parallelism, context isolation, independent verification, or resumable work may materially improve execution.
---

# Agent Orchestration

**Conversation context is disposable. Repository state is durable.**

Choose the simplest execution topology whose expected benefit exceeds its coordination cost.

## Delegation economics

Delegate only for a concrete benefit such as:

- genuine parallelism between independent slices
- context isolation for substantial discovery or implementation
- independent verification where correlated mistakes are costly
- model or cost specialization
- ambiguity reduction that unblocks other work

Account for spawn, reread, handoff, coordination, shared-file contention, and integration cost.

A cohesive task should stay single-core when splitting it would not pay for itself. Do not create fixed Analyst → Builder → Tester → Reviewer ceremonies.

## Safe concurrency

Before parallel implementation:

1. identify real dependencies between slices
2. freeze shared contracts needed downstream
3. assign non-overlapping ownership where practical
4. distinguish conceptual ordering from an actual unresolved dependency
5. define the integration point

Parallelize only when inputs are sufficiently stable and agents will not race on the same state.

## Durable state

Use durable repository state when continuation or cross-agent coordination benefits from it. Do not create process files merely because the template exists.

For complex or long-running work, the full shape may be:

```text
.agents/run/
  assignment.md
  plan.md
  status.md
  findings.md
  handoffs/
    <role-or-slice>.md
```

Use only the files the run needs:

- `assignment.md`: human intent, constraints, acceptance criteria
- `plan.md`: dependency graph, frozen contracts, ownership, integration plan
- `status.md`: current phase, completed work, blockers, exact next action
- `findings.md`: durable discoveries useful across slices or context resets
- `handoffs/*.md`: compressed state for a specific next agent or slice

Delegated work that another agent must consume requires a durable handoff. Tiny cohesive work may need no run files.

After the task, treat `.agents/run/` as ephemeral working state. Promote decisions or findings with long-term value into permanent documentation, ADRs, post-mortems, tests, or other appropriate artifacts rather than preserving a graveyard of coordination files.

## Handoff discipline

Handoffs are not transcripts and must not contain hidden reasoning or chain-of-thought.

Record only decisions, contracts, necessary context, changed areas, validation and exact results, known risks/blockers, and what the next agent needs.

Do not paste source files or large diffs. Git/source is authoritative for implementation details.

## Lead responsibilities

The lead:

- reads current durable state before assigning new work
- uses the minimum economically useful agent topology
- prevents conflicting parallel ownership
- checkpoints contracts before dependent work begins
- integrates results against the original task and active skills
- adds independent verification according to risk, not ritual
- escalates genuine product, architecture, policy, or approval decisions to the user

A fresh lead should be able to resume substantial work from repository instructions, active run state, handoffs, and Git/source without replaying the original conversation.

## Resumption

When resuming:

1. read repository instructions and active assignment/state
2. inspect relevant handoffs and Git/source to verify the checkpoint
3. continue the recorded next action
4. do not redo completed phases solely because conversation context is gone

## Verification

Before finishing delegated work, confirm that delegation earned its cost, required handoffs exist, integration used authoritative source state, and durable findings worth keeping were promoted out of ephemeral run state.
