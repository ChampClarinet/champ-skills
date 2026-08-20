---
name: ownership-boundaries
description: Architecture guidance for assigning state, behavior, side effects, data access, and dependencies to the narrowest meaningful owner. Trigger proactively when implementing or refactoring features with multiple components, modules, dialogs, screens, services, controllers, or workflows; when one parent/object accumulates unrelated state or behavior; when data or callbacks are passed through layers only to reach another owner; or when deciding whether logic should be shared, lifted, extracted, or kept local.
---

# Ownership Boundaries

Keep behavior close to the thing that actually owns it.

This skill is framework-agnostic. It applies to UI components, application modules, services, controllers, domain objects, and other cooperating units.

## Core rule

> Put state, side effects, data access, and behavior at the narrowest meaningful ownership boundary.

Sharing logic does not automatically mean sharing ownership.

A reusable operation may be extracted without centralizing every invocation, lifecycle, or state instance into one parent.

## Before implementing

Identify:

1. **Owners** — which component, module, service, or workflow is responsible for each behavior?
2. **Shared contracts** — which data or actions genuinely need coordination across owners?
3. **Reusable logic** — which operations should be extracted so multiple owners can invoke them independently?

Do not default to the highest common ancestor or a single manager merely because several consumers need similar capabilities.

## Ownership rules

Prefer local ownership when a unit can operate independently.

Keep with the owner:

- local state
- lifecycle-driven effects
- event handling
- loading/error state
- data fetching used only by that owner
- validation specific to that workflow
- mutation state specific to that workflow
- cleanup and subscriptions tied to that owner's lifecycle

Lift or centralize only when coordination is actually required, such as:

- multiple owners must observe the exact same changing state
- an invariant must be enforced across owners
- a shared transaction or workflow coordinates several units
- cache identity or synchronization is intentionally shared
- the platform or framework requires a higher-level owner

## Reuse without accidental centralization

Separate **reusable logic** from **shared state**.

Good reuse often means extracting a hook, service, repository method, helper, or use case that independent owners call themselves.

Do not fetch or compute in a parent solely so children can reuse the result if those children have independent lifecycles and do not require synchronized ownership.

Do not create a central controller simply to avoid duplicate invocations of an already reusable operation.

## Decomposition

Decompose by responsibility, workflow, lifecycle, and ownership — not arbitrary line counts.

Warning signs that a unit may own too much:

- unrelated workflows keep adding state to the same parent or manager
- effects exist only to support one nested child or sub-flow
- callbacks are created in a parent and immediately relayed downward
- data is loaded at a high level even though only one descendant consumes it
- independent dialogs, screens, tabs, or services cannot operate without a central god object
- changing one workflow requires understanding many unrelated states or effects

A large cohesive unit can be healthier than a smaller unit that mixes unrelated ownership.

## Dependency direction

Dependencies should point toward the owner that needs them.

Avoid pass-through layers that receive data, callbacks, or services only to forward them elsewhere. Prefer direct ownership or an intentional shared boundary when the framework permits it.

Do not introduce global state, context, service locators, singletons, or broad managers merely to avoid passing a small number of meaningful dependencies.

## God objects and supercomponents

Treat god objects, god services, and supercomponents as ownership smells, not merely size smells.

A parent should coordinate children when coordination is its responsibility. It should not become the default home for every child's state, effects, queries, and handlers.

Before finishing, ask:

- Does each stateful behavior have a clear owner?
- Are effects and lifecycle logic located with the workflow that requires them?
- Is shared logic reusable without forcing shared state?
- Is any parent or manager carrying behavior only for a child or sub-flow?
- Are any dependencies being relayed through layers without meaningful use?
- Can independent units operate independently where they should?

If not, reconsider the ownership boundary before declaring the implementation complete.

## Framework-specific guidance

When a framework-specific ownership skill exists, use it together with this skill.

This skill determines **who should own the behavior**. Framework-specific skills determine **how to implement that ownership idiomatically**.

For React component architecture, apply `react-component-ownership` together with this skill.

## Interaction with other skills

- `scope-discipline` governs what may change; this skill governs where in-scope behavior belongs.
- `minimalist` should minimize the implementation without using a smaller diff as justification for bad ownership.
- `file-structure` governs file organization; file boundaries should reinforce, not replace, responsibility boundaries.
- framework-specific skills may refine lifecycle, state-management, dependency, and composition patterns.
