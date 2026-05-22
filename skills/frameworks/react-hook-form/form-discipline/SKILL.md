---
name: react-hook-form-discipline
description: React Hook Form guidance focused on form ownership, validation, schema usage, field organization, async submission, and maintainable form workflows.
---

# React Hook Form Discipline

Use React Hook Form for maintainable, performant form workflows.

Forms should keep validation, submission, and state ownership predictable and easy to reason about.

Do not turn forms into giant effect-driven state machines.

## Core Principles

- Prefer explicit form ownership.
- Keep form state local when possible.
- Prefer uncontrolled inputs when practical.
- Centralize validation intentionally.
- Prefer centralized and predictable validation for complex forms.
- Avoid unnecessary form re-renders.
- Keep submission flow easy to trace.
- Keep field responsibility understandable.

## When to Use React Hook Form

Use React Hook Form for:

- non-trivial forms
- validation-heavy forms
- async submission flows
- dynamic forms
- reusable field systems
- multi-field coordination
- forms requiring performance optimization
- schema-based validation
- forms with nested structures

For tiny/simple forms, plain React state may still be simpler.

Do not introduce React Hook Form mechanically for every input.

## Form Ownership

Keep form state ownership local to the form/module whenever practical.

Prefer:

```txt
Form
  -> validation
  -> submission
  -> field state
```

Avoid pushing form state into:

- Redux
- global stores
- unrelated Context providers

unless the form is intentionally part of a larger project-level workflow.

## Validation

Prefer predictable validation ownership.

Centralize validation intentionally.

Validation may use:

- schema validation
- field-level validation
- resolver-based validation
- custom validation logic

depending on project needs and complexity.

Avoid scattering validation rules across:

- JSX
- effects
- submit handlers
- random helper files

Validation should have one clear source of truth.

## Schema Discipline

Keep schemas readable.

Prefer:

- domain-oriented schemas
- reusable field schemas
- explicit validation messages
- predictable transformation rules

Avoid:

- giant impossible-to-read schemas
- deeply magical transforms
- validation logic hidden across many files

## Controlled vs Uncontrolled Inputs

Prefer uncontrolled inputs when practical.

Use controlled inputs only when:

- integrating with controlled UI libraries
- implementing complex formatting/masking
- synchronizing external UI state
- the component requires explicit value ownership

Do not wrap every input in controlled state unnecessarily.

## Field Components

Extract reusable field components when:

- validation UI repeats
- styling repeats
- field structure repeats
- accessibility handling repeats

Good examples:

```txt
form-input
form-select
form-checkbox
form-date-picker
```

Avoid over-abstracting fields too early.

Not every input needs a framework-level abstraction.

## shadcn/ui Integration

Use shadcn/ui form primitives when they improve consistency and readability.

Keep form composition readable.

Avoid deeply nested abstraction layers around shadcn form components.

## Async Submission

Keep async submission flow explicit.

Prefer:

- clear loading state
- explicit success/error handling
- predictable retry behavior
- submission ownership inside the form boundary

Avoid:

- hidden submission side effects
- chained `useEffect` orchestration
- duplicated loading state
- submission logic spread across unrelated files

## Error Handling

Keep validation and submission errors distinguishable.

Prefer:

- field-level validation messages
- form-level submission errors
- explicit server error handling
- predictable reset behavior

Do not hide backend failures behind generic UI messages.

## Reset and Default Values

Use default values intentionally.

Keep reset behavior explicit.

Avoid:

- implicit form resets
- stale default value synchronization
- effect-driven form hydration without clear ownership

If async data initializes the form, make hydration flow understandable.

## Dynamic Forms

For dynamic/nested forms:

- use field arrays intentionally
- keep nested ownership readable
- avoid deeply confusing field paths
- split large dynamic sections into focused components

Avoid giant monolithic dynamic forms.

## Performance

React Hook Form is already optimized for form performance.

Prefer:

- localized field subscriptions
- uncontrolled inputs when practical
- splitting large forms into sections
- avoiding unnecessary watchers

Do not prematurely optimize every field.

## Effects Discipline

Avoid using `useEffect` as form workflow glue.

Prefer:

- explicit submit handlers
- derived values
- schema validation
- controlled ownership boundaries

Use effects only when synchronizing with external systems.

## TypeScript

Use TypeScript-first forms.

Prefer typed schemas and inferred form values:

```ts
interface LoginFormValues {
  email: string;
  password: string;
}
```

Keep form field names type-safe when practical.

Avoid bypassing form typing with `any`.

## Accessibility

Forms should remain accessible.

Prefer:

- labels
- descriptive validation messages
- keyboard-accessible controls
- proper input semantics
- visible error/focus states

Do not sacrifice accessibility for abstraction cleverness.

## Common Anti-Patterns

Avoid:

- giant monolithic form components
- validation logic scattered everywhere
- excessive controlled inputs
- form state in Redux without clear reason
- effect-driven submission workflows
- duplicated validation sources
- hidden async submission logic
- field abstraction frameworks too early
- giant nested field paths that nobody understands
- bypassing TypeScript with `any`

## Review Checklist

When reviewing React Hook Form code, ask:

- Is form ownership clear?
- Is validation centralized?
- Does this really need controlled inputs?
- Is async submission easy to trace?
- Are errors handled predictably?
- Is the form too monolithic?
- Is schema complexity still readable?
- Are effects actually necessary?
- Would another developer understand this quickly?
- Can this form be simpler?
