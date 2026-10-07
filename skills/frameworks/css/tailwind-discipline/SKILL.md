---
name: css-tailwind-discipline
description: Champ's Tailwind/CSS defaults for readable utility composition, reusable variants, theme/layer discipline, motion, and styling-specific traps. Use when implementing or reviewing Tailwind/CSS styling.
---

# Tailwind / CSS Discipline

Use Tailwind as readable project styling, not as a second abstraction language.

Repository-local explicit conventions override these defaults.

## Canonical layout owner

`layout-system` owns structural layout: Grid/Flex preference, spacing hierarchy, responsive width verification, positioning, overflow, container behavior, and arbitrary layout values.

Do not duplicate or weaken those rules here.

This skill owns styling-specific composition around that layout.

## Utility composition

Prefer utilities that keep the rendered structure understandable during review.

Avoid giant unreadable class expressions, duplicated conditional class logic, and helper systems that hide straightforward styling.

Reformat or compose class lists when it improves readability; do not extract styling solely to reduce line length.

## Reuse

Extract reusable styling when repeated appearance represents the same concept and is expected to evolve together.

Prefer established variants, tokens, or shared primitives for repeated component states.

Do not abstract two class lists merely because they currently look similar.

Keep the abstraction at the narrowest shared ownership boundary.

## Arbitrary values

Use arbitrary values for concrete product/design constraints that the normal scale cannot express cleanly.

Do not use them as compensation for a broken layout model or as a substitute for an intentional spacing/token system.

## shadcn/ui

Treat shadcn components as project-owned source code, while preserving upstream structure when compatibility, comparison, or future updates benefit.

Customize when product, accessibility, or maintainability requirements justify it.

Do not mechanically rewrite internals merely to match personal formatting preferences.

## Theme and color

Prefer semantic project tokens/variables when the project has them.

Avoid scattering hardcoded theme overrides when the same semantic role already exists.

Preserve repository dark-mode strategy rather than introducing a second theme mechanism.

## Motion

Use motion for feedback, hierarchy, transitions, or meaningful continuity.

Avoid decorative animation that distracts from interaction.

Prefer transform/opacity for ordinary visual motion when they express the effect; use layout-affecting animation only when the behavior requires it.

## Layering

Avoid ad-hoc z-index escalation.

Use the repository's layer scale when one exists. Otherwise establish the smallest understandable local stacking model rather than competing arbitrary values.

## Accessibility

Styling must preserve usable contrast, visible focus, readable content, touch targets, and native interaction affordances.

Do not remove accessibility cues solely for aesthetics.

## Verification

For touched styling, verify:

- structural decisions still satisfy `layout-system`
- class composition remains readable
- extracted variants represent genuinely shared concepts
- arbitrary values encode real design constraints rather than compensation
- theme and layer behavior use one understandable system
- motion does not obscure interaction
- accessibility affordances remain visible
