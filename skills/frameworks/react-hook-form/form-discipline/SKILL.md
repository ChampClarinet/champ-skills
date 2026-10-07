---
name: react-hook-form-discipline
description: Champ's React Hook Form defaults for form ownership, validation, controlled inputs, async submission, reset behavior, and complex form decomposition. Use for non-trivial React Hook Form workflows.
---

# React Hook Form Discipline

Keep each form's state, validation, submission, and reset lifecycle owned by the form workflow.

Repository-local explicit conventions override these defaults.

## When to use it

Use React Hook Form when a form benefits from coordinated validation, async submission, dynamic fields, reusable field infrastructure, schema integration, or reduced rerender pressure.

Do not introduce it mechanically for trivial input state.

## Ownership

Keep form state local to the form or workflow whenever practical.

Do not promote form state into Redux, broad Context, or an unrelated parent merely to share helpers or avoid prop passing.

A form-oriented component should normally own its validation, submission state, submission errors, and reset lifecycle unless another owner genuinely coordinates the same transaction.

Compose with `ownership-boundaries` and `react-component-ownership`.

## Validation

Give validation one clear source of truth.

For non-trivial forms, prefer a readable schema/resolver boundary when it improves consistency and type safety.

Do not scatter overlapping validation across JSX, effects, submit handlers, and unrelated helpers.

Keep transformations explicit. Avoid schema cleverness that hides what values enter or leave the form.

Distinguish field validation errors from submission/server errors.

## Controlled inputs

Prefer uncontrolled registration when practical.

Use controlled integration when the UI component or workflow genuinely requires explicit value ownership, formatting/masking, or synchronization with external UI state.

Do not wrap every field in controlled state by default.

## Async submission

Keep submission flow explicit and traceable:

`submit → pending → success/error → intentional reset/navigation`

Do not orchestrate submission through chains of effects or duplicate loading state outside the form without a real shared owner.

Preserve useful backend failure information rather than collapsing every failure into a generic form error.

## Defaults and reset

Treat default values and reset behavior as lifecycle decisions.

Avoid implicit resets, stale default-value synchronization, or effect-driven hydration whose ownership is unclear.

When external data can change after mount, define explicitly whether the form should preserve edits, reset, merge, or reject the update.

## Dynamic and large forms

Split large forms by meaningful workflow or ownership sections, not arbitrary line count.

Keep field-array and nested-field ownership understandable. Avoid deeply nested field paths or watcher networks that make update flow difficult to trace.

Subscribe/watch only where the value is actually needed; do not prematurely optimize every field.

## Field abstractions

Extract field components when repeated validation UI, accessibility behavior, styling, or interaction represents the same concept.

Do not build a field abstraction framework before repetition and ownership are clear.

Use shadcn/Radix integration according to the component's actual controlled/uncontrolled contract rather than forcing one model.

## Type and accessibility boundaries

Keep field names and submitted values type-safe. Do not bypass form typing with `any`.

Preserve labels, semantics, keyboard interaction, focus behavior, and understandable validation messages.

## Verification

For touched form behavior, verify:

- form ownership is local unless coordination requires otherwise
- validation has one authoritative path
- controlled fields are controlled for a concrete reason
- submission and reset lifecycle are explicit
- backend errors remain distinguishable from field validation
- external default-value changes have defined behavior
- dynamic sections remain understandable
- effects are not acting as hidden workflow glue
