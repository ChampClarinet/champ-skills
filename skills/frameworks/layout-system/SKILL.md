---
name: layout-system
description: Mandatory layout rules that prioritize Grid, Flexbox, and gap-based structure over spacing hacks and arbitrary offsets.
---

# Layout System

Build layout with layout systems, not with accumulated spacing utilities.

## Non-Negotiable Rules

- Use CSS Grid or Flexbox as the primary mechanism for page, section, and component layout.
- Use `gap-*` for spacing between children inside Grid or Flex containers.
- Do not use `space-x-*` or `space-y-*` as the primary structural layout mechanism.
- Do not build vertical or horizontal page structure by stacking `mt-*`, `mb-*`, `ml-*`, `mr-*`, `pt-*`, `pb-*`, `pl-*`, or `pr-*` across siblings.
- Arbitrary spacing utilities such as `space-y-[...]`, `mt-[...]`, `mb-[...]`, `top-[...]`, `left-[...]`, `translate-x-[...]`, and `translate-y-[...]` must not be used to compensate for an incorrect layout model.
- Prefer alignment primitives such as `items-*`, `justify-*`, `content-*`, `place-*`, `self-*`, and auto-sized Grid tracks over manual offsets.
- Prefer parent-owned layout over child-owned positioning. The parent container should define flow, alignment, and spacing for its children.
- Use margins only for genuine local separation or external spacing where a Grid/Flex `gap` cannot express the intent cleanly.
- Use padding only for a component's internal inset, not to force neighboring components into position.
- Do not use relative positioning, transforms, or negative margins for ordinary document layout.
- If many one-off spacing values are required, assume the layout model is wrong and redesign it with Grid or Flexbox before continuing.

## Tailwind CSS Guidance

Preferred:

```tsx
<div className="grid gap-6 lg:grid-cols-3">
  <SummaryCard />
  <SummaryCard />
  <SummaryCard />
</div>
```

```tsx
<section className="flex flex-col gap-4">
  <SectionHeader />
  <SectionContent />
</section>
```

Avoid:

```tsx
<div className="space-y-[37px]">
  <SectionHeader />
  <SectionContent />
</div>
```

```tsx
<div>
  <SectionHeader />
  <SectionContent className="mt-[43px]" />
</div>
```

```tsx
<div className="relative">
  <Toolbar className="relative top-[8px]" />
</div>
```

Standard Tailwind spacing tokens are still allowed when they represent deliberate local spacing. Arbitrary values require a concrete design requirement that cannot be represented by the project's spacing scale or layout system.

## Reference UI Work

When reproducing a reference image:

- Treat spacing as evidence of the underlying layout, not as isolated pixel offsets.
- Infer rows, columns, alignment groups, container boundaries, and repeated gaps before writing utilities.
- Match the reference with Grid/Flex structure first, then tune a small number of local spacing values only when necessary.
- Do not chase screenshot fidelity by accumulating arbitrary margins, `space-y-[...]`, transforms, or positioned offsets.
- Responsive behavior must come from layout rules and breakpoints, not from compensating offsets.

## Cross-Browser Safety

Layout must remain stable in:

- Chromium-based browsers
- Firefox
- desktop Safari
- iOS Safari

Do not depend on spacing hacks whose result changes with font metrics, intrinsic content height, viewport units, browser rounding, or Safari's layout behavior.

## Required Final Verification

Before completing any task that creates or modifies web UI layout:

- [ ] Inspect every modified container and identify whether Grid or Flexbox owns its layout.
- [ ] Confirm repeated sibling spacing uses `gap-*` where appropriate.
- [ ] Search the final diff for `space-x-[`, `space-y-[`, arbitrary margin/padding values, positional offsets, transforms, and negative margins.
- [ ] For every remaining arbitrary spacing value, confirm it is a documented design requirement rather than compensation for broken structure.
- [ ] Confirm parent containers own child alignment and spacing wherever practical.
- [ ] Verify content growth does not break the layout.
- [ ] Verify the layout at relevant responsive breakpoints.
- [ ] Verify Safari and iOS Safari compatibility for the affected layout.
- [ ] Refactor every spacing hack discovered during verification before reporting the task complete.

Do not report the task as complete while any checklist item fails. A layout that only works because of accumulated spacing offsets is not complete.

## Intent

Optimize for:

- predictable layout behavior
- responsive stability
- cross-browser consistency
- maintainable spacing systems
- clear parent-child layout ownership
- fidelity without pixel-hack accumulation
