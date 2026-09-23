# Agent orchestration

Use this skill when a coding task is coordinated through a lead agent and may delegate work to subagents.

## Core principle

**Conversation context is disposable. Repository state is durable.**

Never make successful continuation of a run depend on the original lead conversation or a subagent transcript. Persist cross-agent coordination state in the repository so a fresh lead can resume safely.

## Execution topology

Choose the simplest safe topology for the task. Do not run a fixed Analyst → Builder → Tester → Reviewer ceremony merely because those roles exist.

Delegation must provide a concrete benefit such as:
- discovery or ambiguity reduction
- context isolation
- independent verification
- genuine parallelism
- model/cost efficiency for a substantial implementation slice

A cohesive, well-understood task may use one implementation agent. Add roles dynamically when the work or risk justifies them.

Lead agents should normally coordinate and evaluate rather than spend expensive reasoning budget on long mechanical implementation, but direct implementation is acceptable for trivial edits, integration glue, or tiny review fixes where delegation overhead would dominate.

## Planning checkpoint

Before dispatching implementation agents, plan for **safe concurrency**, not concurrency for its own sake.

1. Identify the dependency graph between implementation slices.
2. Freeze shared contracts that downstream work needs: API shapes, domain rules, interfaces, ownership boundaries, and other cross-slice assumptions.
3. Assign explicit, non-overlapping file/area ownership where possible.
4. Distinguish a real dependency from a conceptual ordering. Do not serialize a slice merely because another slice is described first; serialize only when it requires unresolved output from the upstream slice.
5. Dispatch all independent, economically worthwhile slices before waiting for any one of them.
6. Record the frozen contracts, ownership, dependencies, and join/integration point in durable run state so parallel agents do not depend on Lead conversation context.

Parallelize only when:
- the downstream inputs are sufficiently frozen,
- agents will not race on the same files/state,
- and expected wall-clock/context savings exceed spawn, reread, and integration overhead.

If those conditions are not met, prefer sequential execution. A tiny independent slice does not deserve a separate agent merely because it could run in parallel.

## Durable run protocol

For an active run, prefer:

```text
.agents/run/
  assignment.md
  status.md
  handoffs/
    <role-or-slice>.md
```

- `assignment.md`: human intent, constraints, and acceptance criteria.
- `status.md`: current phase, completed work, blockers/decisions, exact next action, and relevant handoffs.
- `handoffs/*.md`: compressed state passed between agents.

After every completed phase or delegated result, the Lead updates `status.md` before continuing.

Before finishing delegated work, the agent writes or updates its designated handoff.

A fresh Lead must be able to reconstruct the run from:
1. repository/project instructions
2. `assignment.md`
3. `status.md`
4. relevant handoffs
5. Git/source state

Do not require replaying previous conversation history.

## Handoff discipline

Handoffs are **not transcripts** and must not contain hidden reasoning or chain-of-thought.

Record only:
- decisions and contracts established
- implementation context that cannot be safely inferred
- files or areas changed
- validation performed and exact results
- known issues, risks, or blockers
- information the next agent needs

Do not paste source files or large diffs into handoffs. Git is authoritative for implementation details.

## Lead responsibilities

- Read durable run state before deciding what happens next.
- Use the minimum number of agents that safely completes the task.
- Avoid parallel edits to the same files.
- Sequence work when one slice establishes a contract another depends on.
- Parallelize only genuinely independent work.
- Add independent testing/review based on risk, not ritual.
- Checkpoint state before spawning the next phase.
- If context is lost, resume from durable state instead of restarting completed work.
- Escalate to the human only for a real product/architecture decision or required approval gate.

## Resumption

When resuming an interrupted run:

1. Read project instructions and active assignment.
2. Read `status.md` and referenced handoffs.
3. Inspect Git/source state to verify the checkpoint.
4. Continue the exact next action.
5. Do not redo completed phases solely because their original conversation is unavailable.
