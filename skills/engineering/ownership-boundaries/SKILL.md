---
name: ownership-boundaries
description: Assign state, behavior, side effects, data access, and dependencies to the narrowest meaningful owner. Use when implementing or refactoring cooperating components, modules, services, controllers, or workflows, especially when deciding whether logic should stay local, be lifted, shared, or extracted.
---

# Ownership Boundaries

Put state, side effects, data access, and behavior at the narrowest meaningful ownership boundary.

This skill is framework-agnostic. It determines **who owns behavior**; framework-specific skills determine how that ownership is implemented.

## Ownership model

Before implementing, identify:

1. **Owners** — the unit responsible for each behavior or lifecycle.
2. **Shared contracts** — values or actions that genuinely require coordination across owners.
3. **Reusable logic** — operations multiple owners may invoke independently.

Do not default to the highest common ancestor, global state, or a central manager merely because multiple consumers need similar capabilities.

Sharing logic does not imply sharing ownership.

## Keep behavior local

When a unit can operate independently, keep its concerns with that owner:

- local state
- lifecycle-driven effects and cleanup
- event handling
- loading and error state
- data access used only by that owner
- workflow-specific validation
- workflow-specific mutation state
- subscriptions tied to that owner's lifecycle

Lift or centralize only when coordination is real, such as:

- multiple owners must observe the same changing state
- an invariant spans owners
- one transaction or workflow coordinates several units
- cache identity or synchronization is intentionally shared
- the platform or framework requires a higher-level owner

## Reuse without centralization

Avoid duplicating the same behavior when it represents the same concept and is expected to evolve together.

Extract reusable logic to the narrowest shared abstraction that preserves independent ownership.

Do not abstract merely because two pieces of code currently look similar. Similar syntax is not necessarily shared responsibility.

Sharing logic does not imply sharing state, lifecycle, or ownership.

A hook, service, repository method, helper, or use case may be shared while each owner independently invokes it.

Do not fetch, compute, or mutate in a parent solely to make an operation reusable for otherwise independent children.

Do not create a central controller merely to avoid repeated calls to an already reusable operation.

## Decomposition signals

Decompose by responsibility, workflow, lifecycle, and ownership rather than line count.

Reconsider the boundary when:

- unrelated workflows keep adding state to the same owner
- effects exist only to support one nested workflow
- callbacks are created high in the tree only to be relayed downward
- data is loaded high in the tree for one descendant
- independent dialogs, screens, tabs, modules, or services depend on a central god object
- changing one workflow requires understanding unrelated state or effects

A large cohesive owner can be healthier than several smaller units with mixed responsibility.

## Dependency direction

Dependencies should point toward the owner that uses them.

Avoid pass-through layers that receive data, callbacks, or services only to forward them elsewhere when direct ownership or an intentional shared boundary is available.

Do not introduce global state, context, service locators, singletons, or broad managers merely to avoid passing a small number of meaningful dependencies.

A parent should coordinate children when coordination itself is its responsibility. It should not become the default home for every child's state, effects, queries, and handlers.

## Composition

- `scope-discipline` determines what may change.
- `file-structure` determines where owned units live.
- `minimalist` may reduce implementation size but must not use a smaller diff to justify incorrect ownership.
- framework-specific ownership skills refine this policy for their runtime and lifecycle model.
- for React component architecture, compose with `react-component-ownership`.

## Verification

Before completion, confirm:

- each stateful behavior has a clear meaningful owner
- lifecycle logic stays with the workflow that requires it
- reusable logic is not mistaken for shared state
- parents and managers do not carry behavior solely for independent descendants
- dependencies are not relayed through meaningless layers
- independent units can operate independently where they should
- centralized ownership exists only for a real shared invariant, identity, transaction, lifecycle, or platform requirement
