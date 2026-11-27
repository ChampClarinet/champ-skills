---
name: visual-verification
description: Verify actual rendered appearance when visual correctness is material to acceptance criteria, including layout, wrapping, responsive behavior, layering, and design fidelity.
---

# Visual Verification

Verify the running product, not a representation of what the code should render.

## When to apply

Require visual verification when acceptance depends materially on rendered appearance or motion. Examples include responsive defects, clipping, wrapping, alignment, layering, design fidelity, and visual state transitions.

Do not require it merely because UI files changed. Routine wording changes, nonvisual behavior, and low-risk refactors may use appropriate static or behavioral checks instead.

## Execute

- Identify the visual acceptance criteria and relevant reproduction conditions.
- Use the existing project's runtime and test tools. Prefer targeted checks over new infrastructure.
- Reproduce the affected route, state, data, viewport or device, and interaction. Check relevant boundaries and adjacent states according to risk and repository requirements, not an arbitrary exhaustive matrix.
- Capture actual screenshots for static appearance; use recordings, traces, or suitable runtime measurements for motion or transient behavior.
- Inspect the captured result against the acceptance criteria. A screenshot alone is not a passing assertion. Use behavioral assertions where the claimed outcome also depends on behavior.
- For regressions, capture before/after evidence when practical. Do not fabricate a baseline or require reverting a fix merely to obtain one.

## Evidence and reporting

Record the actual environment, relevant viewport or device, reproduction steps, checked criteria, result, and accessible evidence location. Distinguish pass, fail, and unverified criteria.

Never substitute a mockup, generated image, source inspection, or green build for actual rendered evidence. Do not claim untested devices or states passed.

If runtime access, credentials, capture, or inspection is unavailable, report the limitation and mark the affected criteria unverified. Use the strongest available alternative evidence without claiming equivalent coverage.

Avoid exposing credentials, personal data, or sensitive application content in artifacts. Follow repository artifact and retention rules; do not commit captures by default.

## Composition

This skill owns visual runtime verification, not visual design, implementation scope, general review, or RCA. Compose with `verification` for general acceptance evidence and completion reporting, and with relevant existing skills without duplicating their responsibilities. Supply actual evidence to review and post-mortem records when applicable.

Remain tool-agnostic across web, Flutter, and native applications. Do not install tooling, redesign UI, or expand scope solely to produce evidence without authorization.
