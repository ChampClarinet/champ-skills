---
name: shadcn-ui
description: Registry-first workflow for projects that use shadcn/ui. Use when adding, replacing, or composing UI components in a repository configured with shadcn/ui.
---

# shadcn/ui

Use this skill when the repository uses shadcn/ui or contains a `components.json` shadcn configuration.

## Registry-first workflow

Before implementing a UI primitive or common UI pattern:

1. Inspect `components.json` and the repository's existing local UI primitives.
2. Reuse an appropriate local component when one already exists.
3. If no suitable local component exists, check the **current official shadcn/ui registry and documentation** before writing a custom implementation.
4. Prefer the official shadcn/ui component or documented composition when it satisfies the requirement.
5. Add missing official components through the official shadcn CLI, preserving the repository's existing `components.json` configuration, aliases, styling conventions, and tokens.
6. Prefer composing or extending existing/local official primitives over recreating equivalent behavior.
7. Implement a custom primitive only when the current official registry/documentation has no suitable solution or the product requirement materially differs from the official component/pattern.

Do not rely solely on remembered shadcn/ui component availability. The registry evolves over time, so verify current availability before deciding that a component or pattern must be implemented manually.

Do not install a competing UI/component library merely to avoid using or composing the repository's existing shadcn/ui foundation unless there is a concrete architectural reason.

## Practical checks

When a feature needs UI such as dialogs, confirmation flows, selectors, calendars, command palettes, drawers, forms, navigation, tables, or other common interface patterns:

- Search the local component directory first.
- Check the current official registry/docs second.
- Use the official CLI when adding an available component.
- Customize through composition and the project's design tokens where practical.
- Hand-roll only the behavior that is genuinely project-specific.

The goal is not to force every interface into a stock component. The goal is to avoid maintaining custom equivalents of components that shadcn/ui already provides and maintains.

## Form controls and ownership boundaries

When a project uses `react-hook-form` (RHF), treat RHF and the UI component system as separate concerns:

- RHF owns form state, registration/controllers, validation, submission, and field errors.
- shadcn/ui or the project's local design-system components own the rendered controls and interaction UI.
- Do not interpret "use RHF" as permission to render raw `<input>`, `<select>`, `<textarea>`, date inputs, or hand-rolled pickers when an appropriate local/shadcn component exists or can be added from the official registry.
- Prefer the repository's existing field wrappers and form composition patterns. Use `Controller`/controlled integration only when the chosen UI component requires it.
- Raw native controls are deliberate exceptions, not the default. Use them only when native semantics/capabilities are specifically required or no suitable design-system primitive exists, and make the reason clear in the implementation.

Keep interactive responsibilities separated at meaningful ownership boundaries:

- A page or list may coordinate feature-level data, but should not absorb the internals of every create/edit form, dialog, picker, mutation, and presentation concern.
- Create/edit dialogs or sheets should normally own their own open/form interaction state when that state is local to the interaction.
- Extract forms, dialogs, lists, and independently stateful interactions when doing so creates a clear responsibility boundary.
- Do not create a "supercomponent" merely because several interactions appear on the same screen.
- Also avoid the opposite extreme: do not split trivial markup into one-off components that only add indirection.

Before finishing UI work, explicitly check both questions:

1. Are common controls implemented with the project's local/shadcn primitives rather than raw browser controls without a concrete reason?
2. Does each component have a coherent responsibility, without combining unrelated list, dialog, form, mutation, and presentation ownership?
