---
name: redux-toolkit-state-discipline
description: Redux Toolkit guidance focused on project-level state ownership, slice structure, async state, selectors, Context boundaries, and maintainable Redux usage.
---

# Redux Toolkit State Discipline

Use Redux Toolkit intentionally for project-level shared application state.

Redux should make state ownership predictable, debuggable, and maintainable.

Do not use Redux as the default place for every piece of React state.

## Core Principles

- Use Redux Toolkit for project-level state.
- Keep global state intentional.
- Prefer local state for component-only behavior.
- Prefer React Context for module/component-level coordination when appropriate.
- Avoid Redux for ephemeral UI state.
- Keep slices focused.
- Keep state serializable.
- Prefer typed hooks and typed selectors.
- Avoid `useEffect`-driven workflows when state can be modeled directly.

## When to Use Redux Toolkit

Use Redux Toolkit for:

- project-level shared state
- state shared across distant modules
- app-wide user/session state
- permissions/roles
- cross-page workflow state
- persistent application preferences
- complex state transitions that need traceability
- state that benefits from Redux DevTools
- shared cached server data when RTK Query is the project convention

Use Redux when state needs global ownership, debugging, replayability, or predictable updates.

## When Not to Use Redux Toolkit

Avoid Redux for:

- component-only UI toggles
- local dialog/menu state
- hover/focus state
- local form input state
- animation state
- one-off module state
- state only needed inside one subtree
- temporary state that does not need global visibility

Prefer local state or React Context when the scope is smaller than the project.

## Redux vs Context Boundary

Use Redux for project-level state.

Use React Context for:

- module-level state
- component subtree coordination
- local provider-owned workflows
- state coupled to a specific UI area
- cases where the lifecycle is naturally tied to a subtree

Especially prefer Context/local state when the implementation relies on component lifecycle or `useEffect` behavior.

Do not promote module/component-level state to Redux just to avoid prop drilling.

## `useEffect` Discipline

Do not use `useEffect` chains to simulate global workflows.

React effects should synchronize with external systems, such as browser APIs, subscriptions, timers, or imperative libraries.

If state updates are driven by user events or app actions, prefer explicit event handlers, reducers, or Redux actions.

Avoid patterns where:

- component mounts dispatch project-level workflow actions unnecessarily
- components watch Redux state in effects to trigger unrelated state changes
- multiple effects coordinate business workflows indirectly
- Redux becomes a side-effect event bus

If a workflow requires many component-level effects, reconsider ownership. It may belong in a module Context, custom hook, thunk/listener middleware, or explicit service boundary.

## Store Setup

Use `configureStore` for store creation.

Keep store setup readable and boring.

Prefer:

- clear reducer map
- typed `RootState`
- typed `AppDispatch`
- typed app hooks
- explicit middleware additions
- DevTools defaults unless project policy differs

Avoid:

- custom store setup without reason
- complicated enhancer chains
- hidden middleware behavior
- store config as an architecture dumping ground

## Slice Discipline

Use `createSlice` for Redux state logic.

Slices should represent focused domains or project-level concerns.

Good slice examples:

- `auth`
- `session`
- `permissions`
- `preferences`
- `notifications`
- `workspace`

Avoid slices that become dumping grounds:

- `app`
- `common`
- `misc`
- `data`
- `ui`

unless their scope is intentionally small and well-defined.

## State Shape

Keep Redux state minimal and serializable.

Prefer storing:

- ids
- normalized entities
- primitive state
- serializable objects
- project-level flags
- server cache metadata when appropriate

Avoid storing:

- React components
- functions
- class instances
- DOM nodes
- promises
- controllers
- non-serializable objects

Do not mirror every API response into Redux unless the project needs global access, caching, or derived state.

## Selectors

Use selectors to encapsulate state reads.

Prefer:

- focused selectors
- derived selectors when useful
- memoized selectors for expensive derived data
- stable selector ownership close to the slice/module

Avoid reading deep state paths everywhere.

Good:

```ts
const user = useAppSelector(selectCurrentUser);
```

Avoid:

```ts
const user = useAppSelector((state) => state.auth.session.current.user);
```

when the shape is repeated across the app.

## Actions and Reducers

Reducers should describe state transitions clearly.

Prefer action names that explain intent:

```ts
userLoggedOut;
permissionsLoaded;
workspaceChanged;
```

Avoid vague actions:

```ts
setData;
updateState;
handleChange;
```

unless the slice is intentionally tiny.

Reducers should not contain side effects.

## Async Logic

Use async tooling intentionally.

Options include:

- `createAsyncThunk`
- RTK Query
- listener middleware
- explicit service calls outside Redux when simpler

Use `createAsyncThunk` when:

- async lifecycle needs Redux ownership
- pending/fulfilled/rejected state belongs in Redux
- the result affects project-level state

Use RTK Query when:

- the project standardizes on RTK Query for server cache
- caching/invalidation benefits matter
- API data is shared across the app

Do not add RTK Query casually if the project already uses another data-fetching convention.

## Listener Middleware

Use listener middleware for Redux-owned reactions when needed.

Good use cases:

- reacting to specific Redux actions
- orchestrating project-level side effects
- analytics/logging tied to Redux events
- cross-slice coordination

Avoid using React components and `useEffect` as the main place for project-level Redux orchestration.

Keep listener logic focused and traceable.

## Module-Level State

For module-level flows, prefer local Context or a module provider when:

- the state only matters inside that module
- lifecycle is tied to that subtree
- the flow is UI-heavy
- effects/subscriptions are local to that module
- Redux would make the state unnecessarily global

Module Context should still be explicit and maintainable.

Avoid context spaghetti.

## TypeScript

Use TypeScript-first Redux.

Prefer:

- typed `RootState`
- typed `AppDispatch`
- typed `useAppDispatch`
- typed `useAppSelector`
- typed slice state
- explicit payload types when inference is unclear

Avoid `any` in actions, state, selectors, and thunks.

## Component Integration

Components should:

- select state through selectors
- dispatch intentful actions
- avoid knowing deep store shape
- avoid coordinating large workflows in effects

Keep components readable.

Do not make components responsible for Redux architecture.

## Testing

Prefer testing:

- reducers for state transitions
- selectors for derived state
- thunks/listeners for orchestration
- components with store/provider setup only when UI behavior matters

Avoid relying only on end-to-end tests for Redux logic.

## Performance

Optimize Redux usage based on observed problems.

Prefer:

- focused selectors
- stable state shape
- normalized state where useful
- avoiding giant subscriptions
- splitting components around state reads

Do not prematurely memoize everything.

## Common Anti-Patterns

Avoid:

- putting all React state in Redux
- using Redux for local UI toggles
- dispatching actions from `useEffect` chains without clear ownership
- using Redux as an event bus
- storing non-serializable values
- vague `setData` reducers everywhere
- god slices
- selectors that expose deep state paths everywhere
- duplicating server cache state unnecessarily
- using RTK Query without a project-level reason
- bypassing TypeScript with `any`

## Review Checklist

When reviewing Redux Toolkit code, ask:

- Is this state truly project-level?
- Would local state or Context be simpler?
- Is the slice responsibility focused?
- Is state serializable?
- Are selectors hiding store shape properly?
- Are action names intentful?
- Are side effects outside reducers?
- Is async ownership clear?
- Is `useEffect` being used as workflow glue?
- Can this be simpler?
