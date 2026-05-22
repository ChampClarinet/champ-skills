---
name: css-tailwind-discipline
description: Tailwind and CSS guidance focused on readable utility composition, responsive layouts, maintainable styling patterns, and avoiding CSS chaos.
---

# Tailwind / CSS Discipline

Use CSS and Tailwind to create maintainable, readable, and predictable UI styling.

Styling should support maintainability and product consistency, not become a second programming language.

## Core Principles

- Prefer readability over clever styling tricks.
- Prefer consistency over one-off visual hacks.
- Prefer composition over giant styling abstractions.
- Prefer predictable spacing and layout systems.
- Prefer maintainable responsive design.
- Keep styling understandable during code review.

## Tailwind Philosophy

Use Tailwind as a utility-first styling system.

Prefer:

- composable utilities
- predictable spacing
- consistent layout patterns
- local readability
- shared reusable variants when patterns repeat

Avoid:

- giant unreadable class strings
- random arbitrary values everywhere
- duplicated styling logic
- utility soup
- overengineering design abstractions too early

## Responsive Design

Prefer mobile-first responsive design.

Example:

```tsx
className="
  flex
  flex-col
  gap-4
  md:flex-row
  lg:gap-6
"
```

Prefer responsive behavior that is easy to reason about.

Avoid breakpoint chaos where every screen size behaves differently without a clear pattern.

## Layout Discipline

Prefer modern layout systems:

- flex
- grid

Avoid relying heavily on:

- absolute positioning
- magic margins
- layout hacks

Use spacing systems intentionally.

Prefer:

```txt
gap-4
px-6
py-4
```

over random spacing combinations everywhere.

## Class Readability

Keep class composition readable.

Prefer grouping related concerns:

```tsx
className="
  flex items-center gap-2
  rounded-md border
  px-4 py-2
  text-sm font-medium
"
```

Avoid giant single-line unreadable class chains.

Break long class lists into multiple lines when readability improves or using clsx.

## Reusable Styling

Extract reusable styling patterns when repetition becomes meaningful.

Good candidates:

- button variants
- card layouts
- repeated form layouts
- reusable typography patterns

Do not extract abstractions too early.

Avoid creating giant styling helper systems for small projects.

## Arbitrary Values

Use arbitrary values intentionally.

Acceptable:

```tsx
top-[42px]
```

when:

- integrating with external constraints
- matching precise product requirements
- bridging temporary layout gaps

Avoid arbitrary-value spam that destroys consistency.

Prefer design-system spacing/scales when possible.

## shadcn/ui Discipline

Treat shadcn/ui as owned source code.

You may customize components when:

- product requirements differ
- accessibility needs change
- maintainability improves
- repeated patterns emerge

Do not mechanically rewrite shadcn/ui internals without a clear reason.

Preserve upstream compatibility when practical.

## Dark Mode

Prefer predictable theme handling.

Avoid scattering hardcoded color overrides everywhere.

Prefer shared semantic color usage when the project has design tokens or theme variables.

## Animation

Prefer subtle meaningful motion.

Animation should support:

- feedback
- hierarchy
- transitions
- perceived smoothness

Avoid distracting animation spam.

Prefer performant animation properties such as:

- transform
- opacity

Avoid layout-thrashing animation when possible.

## Z-Index Discipline

Avoid random z-index escalation wars.

Prefer documented layering conventions.

Bad:

```css
z-[999999]
```

Prefer intentional layer scales.

## Overflow / Sizing

Handle overflow intentionally.

Prefer predictable sizing constraints:

```tsx
max - w - screen - lg;
overflow - hidden;
truncate;
```

Avoid layout breakage caused by uncontrolled content growth.

## Accessibility

Styling should not reduce usability.

Prefer:

- sufficient contrast
- visible focus states
- readable font sizes
- accessible spacing/touch targets

Do not remove accessibility affordances purely for aesthetics.

## Performance

Prefer efficient styling approaches.

Avoid:

- excessive DOM nesting for styling only
- unnecessary runtime style generation
- giant unused styling systems
- excessive animation repaint cost

## Review Checklist

When reviewing styling code, ask:

- Is this readable?
- Is spacing/layout consistent?
- Is this responsive behavior predictable?
- Is this abstraction actually reusable?
- Are arbitrary values justified?
- Would another developer understand this quickly?
- Is this maintainable long-term?
- Is accessibility preserved?
