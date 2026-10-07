---
name: react-component-discipline
description: Champ's React + TypeScript component defaults for declaration style, readable JSX, effects, hooks, shared UI, and state-management boundaries. Use when implementing or reviewing project-owned React components.
---

# React Component Discipline

Keep React code explicit, readable, TypeScript-first, and unsurprising.

Repository-local explicit conventions override these defaults.

## Component style

For project-owned components, prefer:

- function components
- `FC<Props>` signatures
- explicitly exported props interfaces
- default export for the primary page/component when repository convention does not say otherwise
- type-only imports where they improve clarity
- descriptive state names such as `isLoading`, `hasError`, `isOpen`, and `selectedId`

Do not turn these syntax preferences into reasons for broad churn in existing code.

`react-component-ownership` owns when a responsibility deserves its own component. `file-structure` owns one-component-per-file and naming policy.

## JSX

Keep JSX declarative and easy to scan.

Move substantial business logic or transformations out of render expressions when they obscure the UI.

Avoid deeply nested ternaries and abstractions that hide rather than clarify rendered behavior.

Extract responsibilities, not markup merely to shorten a file.

## State and effects

Use the narrowest correct owner for state.

Do not introduce global state for component-local UI behavior.

Use effects for synchronization with external systems such as subscriptions, timers, browser APIs, storage, network synchronization, or imperative libraries.

Do not use effects to derive values that can be rendered directly or to simulate business workflows that should be explicit events/state transitions.

Compose ownership decisions with `ownership-boundaries`; use Redux-specific policy only when project-level state is actually involved.

## Hooks

Create custom hooks when they own a coherent reusable stateful/effectful behavior or make a meaningful concern easier to understand.

Do not create hooks merely to move code out of sight.

A hook should expose clear inputs/outputs and should not hide surprising side effects.

Reuse does not imply moving state ownership into the hook when callers should own independent lifecycles.

## TypeScript

Keep component contracts typed.

Prefer interfaces for ordinary component props under Champ defaults; use a type alias when unions, mapped/conditional composition, or another shape makes it clearer.

Avoid `any` except at a deliberate boundary with a concrete reason.

Keep component-local types/helpers colocated when they have no independent ownership; `file-structure` owns extraction policy.

## Tailwind, shadcn, and Radix

Use Tailwind/shadcn/Radix according to repository convention.

Treat shadcn components as project-owned source while preserving upstream structure when compatibility or future comparison/update value matters.

Do not mechanically rewrite shadcn internals without a product or maintainability reason.

`layout-system` owns Grid/Flex, spacing hierarchy, positioning, overflow, and responsive verification.

## Performance

Do not scatter `memo`, `useMemo`, or `useCallback` as ritual.

Add memoization or splitting when there is measured evidence, an observable expensive path, or a clear identity/stability contract that requires it.

Use stable keys that represent item identity.

## Accessibility

Prefer semantic HTML and native interaction semantics.

Preserve labels, keyboard access, visible focus, and accessible control behavior when composing custom UI primitives.

## Composition

- `react-component-ownership`: component responsibility boundaries
- `ownership-boundaries`: general state/behavior ownership
- `file-structure`: files and naming
- `layout-system`: structural UI layout
- `typescript-type-discipline`: non-trivial type policy
- framework adapter: runtime-specific rendering/data behavior

Do not duplicate those canonical policies here.

## Verification

For touched React code, verify:

- component syntax follows repository convention or these defaults
- JSX still exposes behavior clearly
- state is owned at the narrowest correct boundary
- effects synchronize rather than secretly orchestrate
- hooks represent coherent behavior
- memoization has a concrete reason
- accessibility semantics survive composition
