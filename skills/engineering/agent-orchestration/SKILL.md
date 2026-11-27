---
name: agent-orchestration
description: Choose and coordinate single-agent or multi-agent execution for substantial engineering work. Use when delegation, parallelism, context isolation, independent verification, or resumable work may materially improve execution.
---

# Agent Orchestration

**Conversation context is transient. Authoritative durable state enables continuity.**

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

## Risk-based planning

Scale planning effort to the expected cost of being wrong: uncertainty, impact, reversibility, and rework cost. Do not use file count or line count as a proxy, or invent numerical risk estimates.

- For clear, low-risk, reversible work, proceed with a lightweight internal plan; no separate approval or plan artifact is required.
- For non-trivial work, communicate a concise plan covering intended outcome, material assumptions, affected boundaries, and verification.
- Investigate uncertain assumptions before proposing consequential changes. Seek human review of material unresolved decisions, high-impact or difficult-to-reverse changes before implementation, unless explicitly authorized.
- Reassess the plan when evidence invalidates a material assumption or changes risk, scope, or acceptance criteria. Escalate consequential changes rather than silently proceeding.
- Keep planning proportional; use durable plan artifacts only when continuation or coordination benefits.

## Bounded execution

Decompose substantial work into cohesive, independently reviewable outcomes using scope-discipline. Define acceptance criteria, dependencies, and decision authority for each unit. Allow autonomous implementation, verification, and correction within its approved boundary. Resolve minor reversible decisions independently. Obtain human acceptance at meaningful checkpoints before advancing dependent outcomes unless explicitly authorized otherwise.

## Cut-loss policy

Progress, not remaining budget, justifies continuation. Stop unproductive loops even when execution or token budget remains ample.

- Stop when the same failure repeatedly returns without meaningful new evidence, changes oscillate between failed states, or no materially different justified approach remains.
- Reassess structural assumptions rather than accumulating local workarounds.
- Checkpoint before remaining context or execution budget threatens safe completion or a useful handoff, where budget signals are available.
- Do not repeat failed approaches or spawn replacement agents without new evidence or a materially different strategy.
- Apply these rules to single agents, workers, and coordinating agents alike.

## Human escalation

When meaningful progress stalls, request human assistance promptly. A coordinating agent may consolidate a worker's evidence but must not delay human SOS through repeated delegation.

Provide the intended outcome, current failure and evidence, attempted approaches and results, remaining uncertainty, and specific help needed. Preserve completed work and a resumable checkpoint. Resume from that state after human input. Do not claim completion while required criteria remain unresolved.

## Safe concurrency

Before parallel implementation:

1. identify real dependencies between slices
2. freeze shared contracts needed downstream
3. assign non-overlapping ownership where practical
4. distinguish conceptual ordering from an actual unresolved dependency
5. define the integration point

Parallelize only when inputs are sufficiently stable and agents will not race on the same state.

## Context lifecycle

Discover relevant context, not all available context. Start with the task, repository instructions, and known authoritative references; expand only when a material assumption, dependency, or decision requires it. Do not search every connected system by default.

- Distinguish approved intent, observed implementation, historical rationale, and reported progress. Use the source authoritative for the specific claim; current code does not automatically override approved requirements.
- Prefer direct source evidence over copied summaries. Check relevant revision, status, scope, or superseding decisions when freshness matters. Do not treat a recent timestamp alone as authority.
- Reconcile material discrepancies before consequential action. If the authoritative source is unavailable or a conflict remains unresolved, state the limitation and seek human clarification when needed.
- On handoff or resumption, revalidate material assumptions and dependencies against current source state. Replan when they have changed; do not blindly replay stale plans or redo verified work.
- Preserve approved decisions, changed contracts, evidence, and resumable state in the appropriate existing authoritative location when authorized. Update affected records within scope; otherwise report the required reconciliation. Link to authoritative sources rather than duplicating their contents.
- Do not create parallel sources of truth, silently modify external trackers or approved requirements, or persist sensitive session data. Keep discovery and persistence proportional to the task.

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

## Pre-execution handoff

Before implementation begins, capture a durable assignment when substantial discussion, research, or planning has established material context, or when work transfers to another session or agent and that context would otherwise be lost. This includes human-to-agent handoffs. Routine cohesive work with sufficient context needs no separate artifact.

Use the existing assignment.md convention under .agents/run/ or the repository's established equivalent. Reuse an existing assignment rather than duplicating it. Record:

- objective and relevant context with authoritative references
- approved decisions and material rationale
- scope, constraints, and decision authority
- observable acceptance criteria and verification expectations
- unresolved questions, assumptions, and blockers

Distinguish approved decisions from proposals. Do not invent approval, copy whole conversations, or relocate authoritative external records. Include only the context needed for execution.

The receiving agent must read the assignment, validate material assumptions against current authoritative sources, and resolve consequential uncertainties before implementation. Do not repeat settled discussion without new evidence. If the sender cannot write to the repository, provide a portable Markdown handoff and explicitly identify where it should be saved; do not claim it was persisted.

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
2. inspect relevant handoffs and current authoritative sources to verify the checkpoint and material assumptions
3. continue the recorded next action
4. do not redo completed phases solely because conversation context is gone

## Verification

Before finishing delegated work, confirm that delegation earned its cost, required handoffs exist, integration used authoritative source state, and durable findings worth keeping were promoted out of ephemeral run state.
