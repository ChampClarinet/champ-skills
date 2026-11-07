---
name: unslop
description: Audit and refine existing dashboards, apps and web pages that look generic, AI-generated or visually inconsistent. Use for visual polish and anti-slop requests; do not activate for ordinary UI bug fixes or new landing-page strategy.
license: CC-BY-4.0
metadata:
  original-author: Damir Sokolovsky
  source: https://github.com/heydamir/unslop
---

# Unslop

Improve an existing interface by identifying **observable** visual defects and fixing only what matters. The result should feel specific to its product, not merely less decorative.

Adapted from [unslop](https://github.com/heydamir/unslop) by **Damir Sokolovsky**, licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Retain this attribution and link in redistributed adaptations.

## Audit before editing

1. Inspect the relevant UI source and, when feasible, its rendered appearance at desktop and mobile sizes.
2. Record concrete issues with location and evidence: inconsistent spacing, misaligned rows, arbitrary color or radius, noisy shadows, gratuitous glow, meaningless icons, generic copy, weak hierarchy, inaccessible contrast, or motion without purpose.
3. Distinguish **heavy**, **light**, and **no** visual slop. For light slop, patch only observed issues. For no slop, report that honestly; do not redesign.
4. Derive direction from the product: audience, character, domain, one memorable visual moment, and one distinctive detail. Preserve existing brand, copy, information architecture and functional behavior unless the user requests broader changes.
5. If the direction would materially alter the product's identity, confirm it before editing; otherwise implement the scoped refinement.

## Refinement order

- **Spacing and alignment:** establish a consistent rhythm and clear grouping before changing decoration.
- **Color and hierarchy:** respect existing design tokens and semantic status colors; reduce decorative competition.
- **Icons and copy:** unify icon treatment; remove filler, invented claims and unnecessary badges.
- **Typography and layout:** strengthen readable hierarchy and intentional proportions without breaking existing component contracts.
- **Details and motion:** standardize radii and states; use motion only when useful, with reduced-motion support.
- **Visuals:** prioritize real product content over generic gradients or stock-like decoration. Do not purchase or generate assets without authorization.

Treat upstream anti-patterns as **diagnostic signals, not universal bans**. A brand's intentional gradient, playful emoji or display typography may be valid. User intent and repository-local design systems win.

## Verification

Compare before and after against the audit. Verify affected viewports, keyboard focus, contrast, no horizontal overflow, and no unintended behavior or content changes. Report what changed and what remains unverified.

## Composition

- This skill owns **existing-interface visual diagnosis and refinement**.
- `landing-page-design` owns **new conversion-page strategy and initial design**. Load both only if a new page later demonstrates concrete visual problems.
- Use relevant engineering skills for bugs, responsive correctness, component ownership and testing. Do not widen scope into a full redesign by default.
