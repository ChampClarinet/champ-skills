---
name: skill-router
description: Compose champ-skills for non-trivial engineering work by resolving authority, required companion skills, optional overlays, and execution hints without loading unrelated skills.
---

# Skill Router

Compose relevant skills after normal skill discovery. Do not replace discovery with a giant task-to-skill catalogue.

## Authority

Resolve conflicts in this order:

1. platform or system constraints
2. explicit user instructions
3. repository-local instructions and skills
4. champ-skills hard policies
5. champ-skills guidance
6. framework defaults and model judgment

Repository-local explicit policy overrides champ-skills because the active repository owns its conventions. Do not treat an ambiguous or merely existing repository pattern as an explicit override.

When two instructions at the same authority level materially conflict and neither can safely satisfy both, surface the conflict, consequences, and options to the user rather than silently choosing.

## Composition

Load the minimum useful skill set.

For repository modifications, apply `scope-discipline` to govern what may change.

Add canonical engineering skills when their concern is materially involved. Framework skills adapt those principles to framework mechanics; they do not replace or duplicate the canonical owner.

Add optional stance or philosophy skills only when they improve the task. Do not activate a skill merely because a weak keyword match exists.

Prefer one canonical owner for each concern:

- scope: `scope-discipline`
- behavioral ownership: `ownership-boundaries`
- physical component/file policy: `file-structure`
- debugging evidence discipline: `debug-mantra`
- execution topology and delegation: `agent-orchestration`
- actionable touched-surface diagnostics: `tooling-feedback`
- Git/commit discipline: `git-workflow`

## Visual design routing

**Hard routing rule:** whenever a task creates, edits, fixes, reviews, or implements user-facing UI (including components, pages, dashboards, responsive fixes, accessibility fixes, and Figma-to-code), load **at least one applicable design skill** alongside the relevant implementation skills. This is required even if the user did not explicitly ask for visual polish. The design skill must respect the requested scope; loading it does **not** authorize redesign or unrelated styling changes.

Choose the design owner by intent. For analytical dashboards, use `dashboard-design` as the information-architecture owner, `chart-selection` for chart semantics, and `data-viz-review` for explicit audits. Use `unslop` only when general visual consistency or implementation polish is relevant; it does not replace analytical design. Do not automatically load all three visualization skills. Load `landing-page-design` for new conversion-focused marketing pages; otherwise load `unslop` as the lightweight visual-consistency guardrail for existing or general-purpose UI. Do not load both by default. For purely backend, data, or non-UI tasks, neither is required.

- **New conversion-focused landing page, campaign page, waitlist, or marketing hero**: use `landing-page-design` as the design owner. Use framework-specific skills only when their mechanics matter.
- **Existing UI that looks generic, AI-generated, inconsistent, or visually unfinished**: use `unslop` as the visual-audit and refinement owner. Keep product behavior and existing brand unless the user explicitly requests a redesign.
- **New landing page that also needs a polish pass**: `landing-page-design` first; activate `unslop` only if a subsequent review identifies concrete slop. Do not force a second pass.
- **Bug fix, responsive defect, accessibility repair, or Figma-to-code implementation involving UI**: load `unslop` alongside the relevant engineering or implementation skill. Perform only the requested fix; do not expand into a visual redesign.
- **New dashboard or substantial dashboard information-architecture work**: load `dashboard-design`; add `chart-selection` when choosing or changing charts. Add `unslop` only for visual consistency or UI implementation concerns.
- **Chart selection or visualization semantics without dashboard layout work**: load `chart-selection` directly.
- **Chart/dashboard truthfulness or accessibility audit**: load `data-viz-review` directly; add other design skills only when the task calls for fixes.
- **Existing dashboard cosmetic or responsive fix, or general component implementation**: load `unslop` for visual consistency, not `dashboard-design` or `landing-page-design` merely because the component appears on a dashboard.

For any repo modification, retain `scope-discipline`. Existing project tokens, component library, branding, and explicit user constraints outrank either design skill. Avoid duplicate owners for typography, spacing, or visual polish. When the user requests no redesign, avoid expanding the visual scope.

**Discovery caveat:** The always-load rule is enforced only when the agent has discovered and activated this router. Codex can select the new skills automatically only when their `SKILL.md` files are installed in a discoverable skills directory. A router file alone does not install or globally activate them.

## Communication routing

Use `show-me` as a supplementary communication skill, not a design owner or primary implementation workflow.

- Honor explicit requests to use `show-me` within platform and repository constraints.
- Automatically load it when a visual representation materially improves understanding of a complex plan, UI proposal, architecture change, runtime flow, or before/after comparison.
- Consider it when visual input needs interpretation or when the user must resolve a consequential design or engineering choice.
- Skip it for routine changes or when concise prose is equally effective. Do not mandate HTML or visual artifacts.
- Keep visual design routing independent. Show Me does not satisfy the required design skill rule and does not replace runtime verification.

## Late skill activation

Reassess the active skill set when investigation reveals a materially different concern or complexity. Load the minimum useful supplementary skill at that point, even if it was not selected initially. Preserve the primary workflow and authority order.

Reuse instructions already present in context; avoid duplicate loads and recursive routing cycles. Track active skills and their concern owners. Do not claim a skill was loaded if discovery or access failed; report consequential limitations.

## Conflict handling

When active skills appear to disagree:

1. Resolve by authority when possible.
2. A hard invariant beats guidance at the same authority level.
3. If both can be satisfied, compose them.
4. For a low-impact ambiguity, choose the smallest reversible interpretation.
5. For a meaningful unresolved decision, ask the user.

Do not let a framework adapter silently override a repository rule or a champ hard policy.

## Visual verification routing

**Conditional hard rule:** load `visual-verification` when acceptance criteria materially depend on actual rendered appearance or motion. This includes responsive layout, wrapping, clipping, alignment, layering, and design fidelity. Do not activate it merely because UI files changed; routine wording changes and nonvisual behavior do not require it.

Reassess this condition when investigation reveals a visual failure or a visual acceptance criterion not apparent at initial routing. Keep the primary workflow and existing design routing intact. If runtime verification is unavailable, report affected criteria as unverified rather than treating static checks or mockups as equivalent evidence.

## Execution topology

Domain skills may identify separable, parallelizable, or independently verifiable work. They do not prescribe agent counts or fixed roles.

Use `agent-orchestration` when delegation could materially improve parallelism, context isolation, independent verification, or model/cost efficiency. Keep cohesive work single-core when coordination cost would dominate.

For substantial work involving multiple cohesive outcomes, meaningful human checkpoints, or execution-budget risk, apply agent-orchestration even in single-agent mode. Reassess routing when debugging stalls or repeated attempts cease to make progress. Agent-orchestration owns bounded execution, cut-loss, and human escalation; scope-discipline owns decomposition boundaries and structural freedom. Do not require delegation merely to apply these policies.

## Verification

Before finishing non-trivial work, verify that:

- active skills cover the actual concerns, including material concerns discovered after initial routing, and no irrelevant skill drove scope
- repository-local rules won over conflicting personal defaults
- each concern has one canonical policy owner
- optional guidance did not override hard constraints
- unresolved meaningful conflicts were surfaced to the user
- delegation, if used, earned its coordination cost
