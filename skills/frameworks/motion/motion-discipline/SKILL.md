---
name: motion-discipline
description: Motion guidance focused on maintainable animation patterns, transitions, layout animation, gesture handling, and accessible motion systems.
---

# Motion Discipline

Use motion to improve clarity, feedback, hierarchy, and perceived smoothness.

Animation should support the product experience, not distract from it.

Do not turn animation into architecture.

## Core Principles

- Prefer subtle meaningful motion.
- Keep animation ownership explicit.
- Prefer composable animation primitives.
- Prefer maintainable transitions over clever timelines.
- Keep animation close to the UI it belongs to.
- Respect accessibility and reduced-motion preferences.
- Optimize for responsiveness and perceived smoothness.

## When to Use Motion

Use motion for:

- interaction feedback
- transitions
- page/layout continuity
- modal/drawer transitions
- hover/tap feedback
- drag interactions
- loading/skeleton polish
- shared layout transitions
- perceived responsiveness

Avoid animation when it:

- distracts from content
- slows interaction
- reduces readability
- makes state harder to understand
- exists only for spectacle

## Animation Ownership

Keep animation ownership local to the UI boundary that owns the interaction.

Prefer:

```txt
Component
  -> local animation
```

Avoid giant centralized animation orchestration unless the product actually requires it.

Do not push animation state into Redux or project-level state unnecessarily.

## Motion Components

Prefer Motion primitives close to the component they animate.

Good examples:

```tsx
<motion.div />
<motion.button />
```

Avoid excessive wrapper nesting purely for animation.

Keep DOM structure understandable.

## Transition Discipline

Prefer readable transitions.

Good defaults:

- opacity
- transform
- scale
- translate
- layout transitions

Prefer short responsive durations.

Avoid:

- extremely long transitions
- random inconsistent easing
- excessive bounce
- distracting chained sequences

## Layout Animation

Use layout animation intentionally.

Good use cases:

- list reordering
- expandable sections
- modal transitions
- navigation continuity
- shared element transitions

Avoid layout animation everywhere by default.

Too much layout motion creates visual noise.

## Gesture Handling

Use gestures when they improve interaction clarity.

Examples:

- drag
- hover
- tap feedback
- swipe interactions

Avoid gesture overload.

Desktop and mobile interaction expectations differ.

## Exit Animations

Use `AnimatePresence` when exit transitions improve UX clarity.

Good examples:

- modals
- toasts
- menus
- route transitions

Avoid wrapping huge app trees in unnecessary presence orchestration.

## State and Motion

Keep animation state separate from business state whenever possible.

Animation should usually derive from UI state, not own application logic.

Avoid:

- animation-driven workflows
- effects coordinating animation state everywhere
- business logic coupled tightly to animation timing

## Accessibility

Respect reduced motion preferences.

Prefer graceful degradation for users sensitive to motion.

Avoid:

- flashing effects
- excessive parallax
- aggressive movement
- forced motion-heavy experiences

Motion should never reduce usability.

## Performance

Prefer performant animation properties:

- transform
- opacity

Avoid expensive layout/repaint-heavy animation when possible.

Avoid animating:

- width
- height
- box-shadow
- large layout recalculations

unless the UX benefit justifies it.

## Tailwind Integration

Use Tailwind and Motion together intentionally.

Prefer:

- Tailwind for layout/styling
- Motion for animation behavior

Avoid mixing animation responsibility across too many systems.

## Page Transitions

Use page transitions sparingly.

Prefer transitions that:

- preserve orientation
- reinforce navigation flow
- feel responsive

Avoid transitions that slow navigation or obscure content.

## Loading States

Prefer subtle loading transitions over spinner spam.

Good examples:

- skeletons
- fade-ins
- optimistic UI transitions
- layout continuity

Avoid making loading states visually noisy.

## Abstraction Discipline

Extract reusable animation wrappers only when patterns truly repeat.

Avoid building giant animation abstraction systems too early.

Prefer explicit readable motion code first.

## Effects Discipline

Avoid heavy `useEffect` orchestration for animation sequencing.

Prefer declarative motion patterns when possible.

Keep animation flow easy to trace.

## Common Anti-Patterns

Avoid:

- animation everywhere
- giant centralized animation systems
- Redux-driven animation state
- effect-heavy animation orchestration
- random durations/easing
- layout animation spam
- excessive parallax
- distracting motion
- inaccessible motion-heavy experiences
- premature animation abstraction frameworks

## Review Checklist

When reviewing motion code, ask:

- Does this motion improve UX clarity?
- Is the animation distracting?
- Is ownership clear?
- Is this transition maintainable?
- Is performance reasonable?
- Is reduced-motion respected?
- Is this abstraction necessary?
- Would another developer understand this quickly?
- Can this animation be simpler?
