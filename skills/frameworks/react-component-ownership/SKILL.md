---
name: react-component-ownership
description: Apply ownership boundaries to React components, hooks, state, effects, queries, mutations, and interactive workflows. Use when React responsibilities could live at multiple component boundaries.
---

# React Component Ownership

Apply `ownership-boundaries` using React's component and lifecycle model.

## Composition

Use `ownership-boundaries` for the underlying ownership decision and `scope-discipline` when modifying repository state.

Use `file-structure` when creating or extracting component boundaries. Use the active framework adapter when runtime boundaries affect the ownership decision.

Repository-local React conventions override these personal defaults.

## Ownership rules

Keep state, effects, subscriptions, queries, mutations, and handlers in the narrowest component that meaningfully owns their lifecycle and behavior.

A parent coordinates behavior that genuinely belongs to the parent. It should not become the default controller for descendant workflows.

A useful test:

> If this child disappeared, would the parent still need this state, effect, query, mutation, or handler?

If not, prefer ownership by the child or its dedicated abstraction.

Shared state belongs above consumers only when they genuinely coordinate around the same value, identity, transaction, or workflow.

## Reuse

Reusable logic does not imply shared ownership.

Independent components may invoke the same reusable hook or operation while retaining independent lifecycle and state ownership.

Centralize only when shared synchronization, cache semantics, identity, transaction, or workflow behavior requires a shared owner.

## Component boundaries

Dialogs, forms, tabs, tables, sections, cards, and similar feature units are ownership candidates when they carry meaningful independent behavior.

Extract responsibility, not markup. A standalone component should have an ownership, lifecycle, reuse, substantial complexity, testing, or evidence-backed rendering reason beyond shortening the parent.

Performance may justify an additional boundary when profiling or a clear render/dependency model supports it. Do not assume extraction or memoization is automatically faster.

`file-structure` owns the physical file policy after a component boundary is justified.

## Props and dependency flow

Props should express meaningful parent-child contracts.

Repeated pass-through props, parent-owned data used only by a deep child, or bundles of unrelated setters are signals to reconsider ownership. Do not introduce global context merely to avoid a small meaningful prop contract.

## Framework boundaries

React ownership does not override runtime constraints imposed by the active framework.

For Next.js Server/Client Component decisions, establish the desired behavioral owner first, then defer to the Next.js adapter for runtime mechanics. Keep client boundaries narrow when practical, but do not distort ownership merely to eliminate client code.

## Verification

Inspect the resulting ownership graph:

- behavior lives with the lifecycle that requires it
- parents do not carry state, effects, queries, or handlers solely for a child
- reusable logic is not mistaken for shared ownership
- independently operable workflows are not unnecessarily centralized
- props represent real contracts rather than relay chains
- extracted components represent meaningful responsibilities
- performance boundaries have evidence or a clear dependency reason
