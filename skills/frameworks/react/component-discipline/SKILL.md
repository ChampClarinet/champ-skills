---
name: react-component-discipline
description: React + TypeScript component guidance focused on maintainable component boundaries, explicit state ownership, readable JSX, modular architecture, and Tailwind/shadcn-friendly UI structure.
---

# React Component Discipline

Use this skill when creating, reviewing, or refactoring React components.

React code should be TypeScript-first, component-oriented, explicit, and easy to maintain.

## Core Principles

- Use TypeScript for React code.
- Prefer function components.
- Prefer explicit component boundaries.
- Prefer readable JSX over clever abstraction.
- Prefer consistency over novelty.
- Prefer descriptive state names such as `isLoading`, `hasError`, `isOpen`, `selectedId`.
- Keep components focused on one clear responsibility.
- Extract components for readability and reuse, not just to reduce line count.
- Optimize for maintainability and predictable structure.
- Prefer modular organization over generic dumping-ground folders.

## Component Declaration Style

Prefer this component structure for project-owned React components:

```tsx
import { type FC } from "react";

export interface UserCardProps {}

const UserCard: FC<UserCardProps> = (props) => {
  return <div></div>;
};

export default UserCard;
```

## Component Style Rules

- Prefer `FC<Props>` component signatures for consistency across the project.
- Export props interfaces explicitly.
- Keep component naming consistent with filenames.
- Prefer one primary component per file.
- Prefer default export for primary page/component files unless project conventions differ.
- Keep helper types and helper functions close to the component when they are tightly coupled.

## Import Style

Prefer type-only imports when possible:

```tsx
import { type FC } from "react";
```

to reduce runtime imports and improve clarity.

## Component Boundaries

Project-owned components should usually follow one component per file.

A component file may contain:

- the exported component
- small private helper functions
- local constants
- local interfaces/types
- tiny private subcomponents tightly coupled to the parent component

Move subcomponents into separate files when they:

- are reused elsewhere
- become large enough to distract from the main component
- own meaningful state or effects
- need independent testing
- represent a distinct UI concept

Avoid files that become component dumping grounds.

## Project Organization

Prefer module-based organization over generic feature naming.

Use `modules/` for domain or product areas:

```txt
modules/
  auth/
  user/
  billing/
```

Inside a module, organize by responsibility:

```txt
modules/
  auth/
    components/
    hooks/
    services/
    types/
    utils/
```

Prefer atomic-style component grouping for shared UI components:

```txt
components/
  atoms/
  molecules/
  organisms/
  templates/
```

Use atomic categories pragmatically.

Do not force every component into strict atomic theory if a simpler structure is clearer.

## File Naming

Prefer lowercase dash-case filenames:

```txt
user-profile-card.tsx
```

Keep filenames aligned with component names and responsibilities.

Use existing project conventions when already established.

## TypeScript Usage

Use TypeScript for all React code.

Prefer explicit props typing:

```tsx
import { type FC } from "react";

export interface UserCardProps {
  name: string;
  isActive?: boolean;
}

const UserCard: FC<UserCardProps> = ({ name, isActive = false }) => {
  return <div>{name}</div>;
};

export default UserCard;
```

Prefer interfaces for component props unless a type alias is clearer for:

- unions
- intersections
- utility types
- mapped types

Avoid `any` unless there is a deliberate boundary and a comment explaining why.

Avoid enums for simple UI states.

Prefer literal unions:

```ts
type Status = "idle" | "loading" | "success" | "error";
```

## TypeScript File Separation

Keep small component-local types, constants, and helpers inside the component file when they are tightly coupled and do not distract from readability.

Extract TypeScript files when they are:

- reused by multiple files
- large enough to distract from the component
- domain-level concepts
- API/data contracts
- validation schemas
- shared constants
- shared helpers

Common extraction patterns:

```txt
user-card.tsx
user-card.types.ts
user-card.constants.ts
user-card.helpers.ts
```

or module-level:

```txt
modules/
  auth/
    auth.types.ts
    auth.constants.ts
    auth.helpers.ts
```

Avoid dumping unrelated exports into broad files like:

```txt
types.ts
utils.ts
constants.ts
```

unless they are small, cohesive, and clearly scoped to the module.

## JSX Discipline

Keep JSX declarative and readable.

Prefer:

- clear conditional rendering
- small derived variables for readability
- descriptive component names
- simple composition

Avoid:

- deeply nested ternaries
- large inline business logic inside JSX
- complex data transformations directly inside render
- clever abstractions that hide UI behavior
- giant render blocks with mixed responsibilities

## State Ownership

Keep state as local as possible.

Use local component state for:

- UI toggles
- controlled inputs
- local dialog/menu state
- transient interaction state
- purely visual UI behavior

Lift state only when multiple components need coordination.

Do not introduce global state for one component's local UI behavior.

Prefer simpler local state before introducing external state management.

## Effects Discipline

Use effects intentionally.

Effects are for synchronizing with external systems such as:

- browser APIs
- subscriptions
- timers
- imperative third-party libraries
- network/storage synchronization when required

Avoid using `useEffect` to derive state that can be computed during render.

Avoid effect chains that simulate business workflows.

Prefer:

- derived values
- explicit event handlers
- framework-native async/data patterns

over effect-heavy orchestration.

## Hooks Discipline

Prefer custom hooks when logic is:

- reused
- stateful
- effect-heavy
- difficult to read inline

Custom hooks should usually:

- encapsulate one concern
- expose clear inputs/outputs
- avoid hidden side effects
- avoid becoming mini-frameworks

Avoid creating hooks solely to move code around mechanically.

## Tailwind / shadcn / Radix

Current preferred UI stack:

- Tailwind CSS
- shadcn/ui
- Radix UI when needed

Use Tailwind for layout and styling when it keeps markup readable.

Use shadcn/ui as owned source code, not untouchable vendor code.

Preserve shadcn/ui structure when:

- maintaining upstream compatibility
- preserving component composition
- reducing unnecessary churn

Do not mechanically rewrite shadcn/ui internals unless there is a clear maintainability or product reason.

## Styling Discipline

Prefer:

- responsive mobile-first layouts
- readable utility composition
- consistent spacing
- shared reusable variants when patterns repeat
- project design tokens when available

Avoid:

- huge unreadable class strings
- duplicated variant logic everywhere
- random spacing systems
- premature design-system abstraction before patterns stabilize

## Performance

Optimize based on observed problems, not fear.

Prefer:

- stable keys
- reasonable component boundaries
- avoiding unnecessary global state
- lazy loading when appropriate
- splitting expensive areas intentionally

Do not scatter:

- `memo`
- `useMemo`
- `useCallback`

everywhere by default.

Memoization should solve a measured or observable problem.

## Accessibility

Prefer accessible defaults.

Use semantic HTML when possible.

Prefer:

- proper button elements
- labels for inputs
- keyboard-accessible interactions
- visible focus states

Do not sacrifice accessibility for visual cleverness.

## Review Checklist

When reviewing React code, ask:

- Is the component responsibility clear?
- Is state owned at the correct level?
- Can this be simpler?
- Is JSX readable?
- Are effects actually necessary?
- Is TypeScript helping instead of being bypassed?
- Is styling consistent with the project?
- Is this abstraction solving a repeated problem?
- Would another developer understand this quickly?

## Shared Components vs Modules

Use `components/` for reusable cross-module UI building blocks.

Examples:

```txt
components/
  atoms/
  molecules/
  organisms/
  templates/
```

Use `modules/` for domain/product/business areas.

Examples:

```txt
modules/
  auth/
  profile/
  checkout/
  dashboard/
```

A module may contain:

```txt
modules/
  auth/
    components/
    hooks/
    services/
    types/
    utils/
```

Module internals are scoped to that domain unless intentionally shared globally.

## State Management Philosophy

Prefer state ownership at the smallest reasonable scope.

Use:

- local component state for component-local behavior
- React Context for module/subtree-level coordination
- Redux Toolkit for project-level shared application state

Do not automatically promote local or module state into Redux.

Prefer React Context when:

- the state belongs to one module/subtree
- lifecycle is tied to a subtree
- effects/subscriptions are local
- the workflow is UI-heavy
- global visibility is unnecessary

Prefer Redux Toolkit when:

- state is project-level
- multiple distant modules depend on it
- debugging/replayability matters
- the workflow benefits from centralized predictable updates

Avoid turning Redux into a global event bus.

Avoid Context spaghetti with deeply nested unclear providers.

Choose the smallest ownership boundary that keeps the system maintainable.
