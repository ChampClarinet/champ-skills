# Redux Toolkit skills

Redux Toolkit state management guidance for project-level app state, store structure, slices, async flows, selectors, and maintainable Redux usage.

Redux Toolkit skills should keep global state intentional, predictable, type-safe, and easy to debug.

## Philosophy

- Use Redux Toolkit for project-level shared state
- Keep global state intentional
- Prefer local state or React Context for module/component-level state
- Avoid Redux for ephemeral UI state
- Avoid `useEffect`-driven component workflows when state ownership belongs elsewhere
- Prefer explicit slices, typed hooks, selectors, and clear update paths
- Keep Redux state serializable and debuggable

## Skills

- **[state-discipline](./state-discipline/SKILL.md)** — Redux Toolkit guidance focused on project-level state ownership, slice structure, async state, selectors, Context boundaries, and maintainable Redux usage.
