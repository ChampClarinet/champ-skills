---
name: management-talk
description: Reframe engineering content for engineering-org leadership and shape it for JIRA, Slack, async standup, email, or meeting talking points. Use for leadership/status updates, executive summaries, less-technical rewrites, or channel-specific versions of engineering work.
---

# Management Talk

Translate engineering truth for engineering-savvy leadership without losing state, impact, ownership, tracking references, risk, or next action.

This is a reframe, not a new analysis. Never improve the story by inventing certainty or facts.

Use `post-mortem` as the canonical engineering record when one exists; this skill changes audience and channel, not the underlying truth.

## Audience boundary

The default audience is engineering-org leadership: VPs, directors, PMs, release managers, and technical executives who understand product and concept-level engineering vocabulary but do not need code-level mechanics.

For materially different audiences such as customers, marketing, finance, or a true ELI5 explanation, adapt deliberately rather than assuming this abstraction level fits.

## Translation rules

### Keep

Preserve facts that let leadership understand or track the work:

- current state and impact
- product, framework, service, or team-owned component names
- customer or workload identifiers
- JIRA/ticket keys and PR numbers
- owner when known
- mitigation, risk, blocker, decision point, and next step when relevant

### Strip

Remove implementation identifiers that do not change the leadership decision:

- function and variable names
- file paths and line numbers
- struct fields and code expressions
- commit SHAs
- low-level debugging mechanics

Keep one only when that exact identifier is itself operationally or organizationally important.

### Translate

Convert mechanism into concise cause and effect without changing its meaning.

Keep useful concept-level vocabulary such as race condition, synchronization, regression, queue, driver, kernel, fast-path, or workaround when it communicates the problem accurately.

Do not replace precise concepts with vague language merely to sound non-technical.

## Framing

Lead with the information that changes what the audience knows or does.

Normally prioritize:

`state → impact → owner/blocker → next step`

Add mechanism, mitigation, risk, or escape-path context only when it changes understanding or a decision.

Use active voice, concrete subjects, and short paragraphs.

Do not:

- hide uncertainty behind confident prose
- add unsupported hedging
- narrate debugging minutiae unless the process itself is the relevant lesson
- restate obvious product background for completeness
- tell leadership what decision to make unless the user asked for a recommendation

## Channel shapes

Preserve the same underlying facts while changing density and presentation for the destination.

### JIRA / written status

Use a scan-friendly structured update.

Useful blocks, ordered by relevance:

- **Status / TL;DR** — one line that gives the correct state
- **Impact** — who or what is affected and how
- **What broke** — short plain-English mechanism
- **Why now / escape path** — only when materially useful
- **Owner / blocker** — known ownership or dependency
- **Next steps** — concrete near-term progression
- **Mitigation / workaround** — when users are affected now
- **Risk** — real risk only; do not manufacture one

Do not force every block into every update.

### Slack

For a top-level channel post:

- lead with a concise TL;DR
- follow with only the few facts needed for impact, ownership, blocker, or next step
- prefer one useful tracking link/reference over a link wall
- avoid JIRA-shaped walls of labeled sections

For a thread reply, lead directly with the answer rather than repeating a TL;DR.

As a default, keep a top-level update around 80 words or less and a thread reply around 40 words or less unless the situation needs more context.

### Async standup

Use 1–3 lines.

Prefer:

`state + thing → owner/blocker if relevant → next step`

Front-load the verb. Do not reproduce a full status report.

### Email

Make the subject carry the state or decision-relevant headline.

Use a small number of flowing paragraphs rather than transplanting JIRA section labels.

End on the next decision, dependency, or action when one exists.

### Meeting talking points

Write for speech:

- one short clause per bullet
- order bullets in speaking order
- retain numbers, ticket keys, or identifiers the speaker needs to reference aloud
- avoid prose paragraphs

## Source handling

Use the strongest available engineering source: a canonical post-mortem, ticket, pasted technical text, repository evidence, or the current conversation.

Prefer the latest substantive state over dumping history.

If sources conflict, do not silently reconcile them. Preserve the conflict or resolve it from evidence before writing the update.

If the requested channel or audience materially changes the output and cannot be inferred, ask one focused question.

## Safety against information loss

Before removing a technical detail, ask whether its removal changes any of these:

- the actual state
- severity or affected scope
- causal meaning
- ownership
- mitigation or workaround
- risk
- blocker or dependency
- tracking continuity
- next action or decision

If yes, preserve or translate it rather than stripping it.

## Verification

Before finalizing, confirm:

- the leadership version does not contradict the engineering source
- uncertainty remains uncertainty
- impact is expressed in user, workload, product, or delivery terms where possible
- important ticket/PR/customer/workload references remain
- owners are not invented
- mechanism is understandable without unnecessary code identifiers
- channel density matches where the update will be consumed
- mitigation, risk, blocker, and next step appear only when supported and relevant
- the rewrite reports status rather than smuggling in an unsolicited recommendation
