---
name: scrutinize
description: Outsider-perspective end-to-end review of a plan, PR, diff, or code change. Question whether the change should exist, consider simpler alternatives, trace the real path beyond the diff, and verify each claim with evidence. Use for reviews, audits, sanity checks, and second opinions.
---

# Scrutinize

Stand outside the change. Ask whether it should exist at all, then verify end to end that it does what it claims.

## Stance

- **Outsider** — evaluate the artifact rather than defending its author's intent.
- **End-to-end** — the diff is an entry point, not the execution boundary.
- **Simpler when better** — always consider whether existing or smaller machinery solves the same problem.
- **Evidence-backed** — every finding explains the consequence and evidence, not merely a preference.

## 1. Establish intent

State the intended outcome in one sentence.

If the artifact is too underspecified to establish its goal, say what is missing before pretending to verify it.

Run one simpler-alternative pass:

- Is doing nothing valid because the problem is not real or load-bearing?
- Does the repository already contain machinery that solves it?
- Can a smaller change achieve the required outcome with less risk?
- Does the problem belong at another layer such as configuration, framework, build, or runtime?
- Is new complexity buying a concrete capability?

If a materially better alternative exists, surface it before lower-level findings.

Skip this challenge only when the user explicitly asks not to question scope or approach.

## 2. Trace reality

For each claimed behavior, follow the actual relevant path beyond the changed lines:

`entry → calls → branches → state/effects → observable result`

Inspect unchanged code at the seams when it affects the behavior.

For plans and designs, trace the proposed flow against the existing system and identify assumptions that do not match reality.

Unexpected branches, ownership, state, or dead/reachable paths are evidence worth investigating.

## 3. Verify claims

For each important claim, distinguish:

- what the artifact says
- what the traced path demonstrates

Check relevant failure surfaces such as error paths, partial failure, retries, concurrency, ordering, empty or extreme inputs, and contract changes according to the actual change.

Check silent effects on performance, error semantics, observability, callers, persistence, or wire formats when relevant.

Verify that tests exercise the behavior being claimed rather than only an intermediate state or mocked path.

Do not manufacture generic edge cases merely to make the review look exhaustive.

## 4. Report

Order findings by severity: blocker → major → minor → nit.

For each finding provide:

- **Finding** — specific issue and location when applicable
- **Why it matters** — concrete consequence
- **Evidence** — traced path, observed behavior, or reproducible condition
- **Suggested change** — smallest useful correction

Close with a concise verdict such as ship, fix-then-ship, rework, or reject, with the main reason.

If no defect is found, state what paths and claims were actually checked rather than emitting a content-free LGTM.

## Verification rules

- Cite concrete code paths, files, lines, or other inspectable evidence for code claims when available.
- Do not confuse a PR or plan's claim with independent verification.
- Do not bury structural problems under style nits.
- Do not add unsupported certainty.
- Keep findings concise and actionable.
