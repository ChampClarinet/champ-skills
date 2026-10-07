---
name: redux-toolkit-state-discipline
description: Champ's Redux Toolkit policy for project-level state ownership, Context boundaries, slices, async orchestration, selectors, and serializable state. Use when deciding whether state belongs in Redux or implementing Redux Toolkit behavior.
---

# Redux Toolkit State Discipline

Use Redux Toolkit for intentionally project-level shared application state, not as the default home for React state.

Repository-local explicit conventions override these defaults.

## Ownership boundary

Prefer:

- local component state for component-owned behavior
- React Context/provider ownership for module or subtree coordination
- Redux Toolkit for project-level state shared across distant modules or workflows

Do not promote state to Redux merely to avoid prop drilling.

Redux is appropriate when global ownership, cross-page coordination, traceable transitions, replay/debugging, persistent application preferences, or project-wide identity/session/permission state materially benefit.

Ephemeral UI state, local forms, animation state, and subtree-only workflows normally stay outside Redux.

Compose with `ownership-boundaries`; this skill maps that ownership into Redux mechanics.

## Slice discipline

Slices should represent focused project-level domains or concerns.

Avoid dumping-ground slices such as `app`, `common`, `misc`, `data`, or broad `ui` when a meaningful domain owner exists.

Keep Redux state minimal and serializable. Do not store React elements, DOM nodes, functions, promises, controllers, or arbitrary class instances.

Do not mirror every API response into Redux merely because it can be stored there.

## State access

Use focused selectors as the read boundary rather than teaching components the deep store shape.

Use derived or memoized selectors when they encode reusable derivation or avoid meaningful expensive work. Do not memoize everything by default.

Components should dispatch intentful actions and avoid coordinating project-level workflows through chains of effects.

## Async ownership

Choose async machinery according to ownership:

- use RTK Query when it is the project's server-cache convention and shared caching/invalidation is valuable
- use thunks when pending/fulfilled/rejected lifecycle belongs to Redux
- use listener middleware for Redux-owned reactions and cross-slice orchestration
- keep service calls outside Redux when Redux ownership adds no value

Do not introduce RTK Query beside another established server-state convention without a project-level reason.

Do not use Redux as an event bus or React `useEffect` chains as hidden Redux orchestration.

Reducers remain side-effect free.

## Context boundary

Prefer Context/provider ownership when state belongs to one module/subtree, lifecycle follows that subtree, or effects/subscriptions are local to it.

Context is not automatically better than Redux: avoid provider spaghetti and unclear ownership.

The decision is scope and lifecycle, not which API requires fewer lines.

## Type safety

Use typed store boundaries, dispatch, selectors, slice state, and payloads.

Do not bypass Redux contracts with `any`.

## Verification

For touched Redux behavior, verify:

- the state genuinely requires project-level ownership
- a smaller local/provider boundary would not own it more accurately
- slices represent meaningful domains rather than dumping grounds
- stored values are serializable unless repository policy explicitly supports an exception
- selectors hide unnecessary store-shape knowledge
- async orchestration has a clear owner
- effects are not being used as an indirect event bus
- server state is not duplicated without a caching or ownership reason
