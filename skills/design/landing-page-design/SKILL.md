---
name: landing-page-design
description: Design and build new conversion-focused landing pages, marketing pages, campaign pages, waitlists, and marketing hero sections. Use when the primary outcome is a new page with a clear audience, offer and CTA; not for routine app UI, bug fixes or general components.
---

# Landing Page Design

**Goal:** one offer, one audience, one primary action. Use this skill as the canonical design owner for a new conversion-focused page. Apply `scope-discipline` when editing a repository.

Adapted for champ-skills from [elayadesign/ai-design-skills](https://github.com/elayadesign/ai-design-skills/tree/main/skills/landing-page-design) (MIT). Preserve upstream credit for the source's adaptation of [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) (MIT).

## Decide before building

- Establish the offer, target audience, conversion action, key objection and available proof. Read existing product and brand material first.
- Ask only for missing facts that materially block a sound result. Otherwise state assumptions briefly and proceed.
- Pick a page structure for the audience and traffic intent: direct offer, narrative, comparison or short waitlist. Do not mechanically add every possible section.
- Prefer specific, verifiable benefit copy over hype. Do not invent testimonials, metrics, customer logos, guarantees or product capabilities.
- Select a single primary CTA; secondary actions must not compete with it.

## Build

1. **Content first.** Write the hero's outcome-led headline, supporting explanation, CTA and truthful proof. Sequence later sections around objections and evidence.
2. **Design system second.** Inspect repository tokens, brand, fonts, components and spacing. Reuse them before inventing values. Choose a coherent type scale, grid, spacing rhythm and radius hierarchy.
3. **Visual direction.** Give the page a product-specific visual idea; use authentic product imagery or an accurate UI preview when available. Do not add decorative images just to fill space.
4. **Implementation.** Follow the existing stack and component boundaries. Keep interactions functional, keyboard accessible and respectful of reduced motion.
5. **Verification.** Check copy claims, CTA destination, metadata, semantic structure, mobile viewport, overflow, contrast, focus states and responsive layouts. Report checks that could not be run.

## Composition

- This skill owns landing-page strategy, copy hierarchy and visual direction.
- Framework and engineering skills own implementation mechanics, testing and code boundaries.
- Use `unslop` as a **conditional follow-up** only when the rendered result shows specific generic-AI visual defects. Do not auto-load it.
- For existing product UIs needing only visual refinement, use `unslop` instead.
- Explicit project design systems and user instructions override aesthetic defaults.

## Completion

Deliver the implemented page or requested artifact, concise design rationale, verification evidence and any unresolved assumptions. Avoid mandatory animation or ornamental sections without a product reason.
