---
name: file-structure
description: Champ's project-owned component, widget, class, and TypeScript file organization policy. Use when creating, extracting, moving, or reorganizing these units.
---

# File Structure

Repository-local explicit rules override this personal default.

## Hard invariants

### React

Exactly one project-owned React component per file.

Private, nested, local, helper, and non-exported components are not exceptions. Do not evade the rule by turning a meaningful component into a substantial JSX-returning render function, callback, or component factory.

A route, page, layout, or logical entrypoint may remain its file's single primary component. Do not create meaningless pass-through components merely to satisfy the rule.

A genuine upstream shadcn/ui file may retain its upstream multi-component structure only when provenance is clear and preserving that structure materially supports upstream comparison, updates, or compatibility. Project-owned wrappers, variants, composites, and feature components do not inherit this exception.

### Flutter

Exactly one project-owned Flutter widget per file.

A `StatefulWidget` and its single matching `State<T>` implementation stay together and count as one widget unit. This also applies to equivalent framework pairs such as `ConsumerStatefulWidget` + `ConsumerState<T>`. Additional widgets must be extracted.

### Domain classes

Keep one primary project-owned domain, service, or model class per file. Do not use this rule to split tightly coupled implementation details that are not independently owned units.

## Extract responsibility, not markup

One-component-per-file does not mean every JSX fragment deserves a component.

Create a component when it represents a meaningful responsibility, ownership boundary, independent reuse, lifecycle/state boundary, substantial rendering complexity, or evidence-backed performance boundary.

Keep tiny tightly coupled presentation as inline JSX or a small render helper.

Do not use line count, visual neatness, or reduced parent length as the extraction rule.

Use `ownership-boundaries` and `react-component-ownership` when the ownership decision itself is unclear.

## Colocation

Keep supporting declarations that belong only to one component with that component by default, including local props/types, schemas, constants, event types, lookup maps, and small non-rendering helpers.

Extract supporting code only when it has an independent domain/API/application ownership, multiple independent consumers, a substantial separate maintenance responsibility, or a repository/framework requirement.

One component per file does not mean one declaration per file.

## TypeScript / TSX naming

For project-owned TypeScript and TSX, use lowercase `kebab-case` for the subject. Use semantic dot-role segments when they improve navigation.

Examples:

```text
stock.card.tsx
stock.table.tsx
create-stock.form.tsx
borrow.dialog.tsx
summary-section.tsx
```

Do not apply this naming policy to generated/vendor files or unrelated languages.

## Logical folders and entrypoints

Use `index.ts` or `index.tsx` when a folder represents a meaningful logical unit with several related files and the index is its entrypoint or composition surface.

Do not create an index wrapper for every folder by habit. An entrypoint must not become a dumping ground for child-specific state, effects, queries, or implementation details.

## Verification

Before completing a task that creates or modifies project-owned React or Flutter UI, inspect the touched files and confirm:

- each project-owned React file has exactly one React component
- component extraction represents a real boundary rather than component confetti
- component-local supporting declarations remain colocated unless independently owned
- touched project-owned TypeScript/TSX filenames follow the naming policy
- logical entrypoints have a real structural purpose
- each Flutter file has exactly one widget unit, with only its matching state implementation as the stateful-pair exception
- any retained multi-component shadcn/ui file has genuine upstream provenance and still benefits from preserving upstream structure

A detected violation in touched in-scope code is required correction before completion, not an optional follow-up. Do not expand scope into untouched unrelated files solely to enforce this policy.
