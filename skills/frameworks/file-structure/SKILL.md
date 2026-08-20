---
name: file-structure
description: Mandatory file organization rules for maintainable component and class structure, including TypeScript semantic filenames and logical entrypoint folders.
---

# File Structure

Use one primary class or component per file.

## Non-Negotiable Rules

- Exactly one project-owned Flutter widget per file.
- Exactly one project-owned React component per file.
- One domain, service, or model class per file.
- Never group multiple project-owned React components in one file, even when they are small, private, closely related, used only once, or compose a single screen.
- Extract every additional project-owned React component into its own file and import it.
- Do not treat non-exported, nested, helper, local, or subcomponents as exceptions. If a function or variable is used as a React component, it is a component for this rule.
- Do not evade the React rule by converting a component into a `renderX`, `getX`, JSX-returning callback, or component factory. A substantial UI section with its own responsibility must be extracted into its own component file.
- Avoid grouping unrelated classes or components in the same file.
- Avoid "misc", "utils", or "components" files becoming dumping grounds.

Terms such as "prefer", "when practical", file size, convenience, locality, or reduced import count must not weaken these rules. For project-owned React code, one component per file is a completion requirement.

Non-component helpers, hooks, types, constants, and data may remain alongside the file's single component when they are tightly coupled to it. They must not render JSX or be used as React components.

A route, page, or layout may remain the single primary React component in its own file. Do not create a redundant pass-through wrapper merely to satisfy this rule.

## TypeScript / TSX filename convention

These naming rules apply to project-owned TypeScript and TSX files only. Do not copy this convention into Dart, Flutter, or unrelated languages unless that language's own conventions explicitly call for it.

Use lowercase `kebab-case` for the subject name. Use `.` segments to express what the file is when that distinction improves navigation.

Examples:

```txt
stock.card.tsx
stock.table.tsx
create-stock.form.tsx
create-stock.dialog.tsx
borrow.dialog.tsx
return.dialog.tsx
summary-section.tsx
```

The file name does not need to mirror the PascalCase React identifier literally. For example:

```txt
stock.card.tsx        -> StockCard
create-stock.form.tsx -> CreateStockForm
summary-section.tsx   -> SummarySection
```

Use hyphens inside the subject when it contains multiple words, and reserve `.` for a meaningful role or artifact kind.

For example:

```txt
create-stock.dialog.tsx
stock-transaction.table.tsx
employee-selector.form.tsx
```

Use the dot segment for a meaningful role or artifact kind such as:

- `.card`
- `.table`
- `.form`
- `.dialog`
- `.hook` only when that matches existing repository conventions
- another clear domain-specific role when it makes the file easier to locate

Do not force a dot suffix when the subject name is already clear. A name such as `summary-section.tsx` is valid when `summary-section` is itself the meaningful component name.

Avoid snake_case component filenames such as:

```txt
create_stock.form.tsx
summary_section.tsx
stock_transaction.table.tsx
```

Prefer:

```txt
create-stock.form.tsx
summary-section.tsx
stock-transaction.table.tsx
```

Avoid vague names such as:

```txt
component.tsx
item.tsx
helper.ts
misc.ts
utils.ts
```

when a more specific subject-and-role name is available.

## TypeScript logical folders and `index` entrypoints

Use `index.ts` or `index.tsx` when a logical TypeScript unit has grown into multiple related files and the index is the entrypoint or composition surface of that unit.

Typical shape:

```txt
stock.tab/
  index.tsx
  stock.table.tsx
  details.dialog.tsx
  edit.dialog.tsx
```

Here, `stock.tab/index.tsx` is the entrypoint for the StockTab zone. It should compose or expose the unit while the detailed responsibilities live in sibling files.

Another example:

```txt
stock/
  index.tsx
  header.tsx
  stock.card.tsx
  create-stock.dialog.tsx
  create-stock.form.tsx
  stock.tab/
    index.tsx
    stock.table.tsx
    details.dialog.tsx
    edit.dialog.tsx
  transaction.tab/
    index.tsx
    transaction.table.tsx
    details.dialog.tsx
```

Use an index entrypoint when:

- the folder represents one meaningful zone, component, or module
- that unit needs several files to stay maintainable
- consumers should interact with the unit through its primary entrypoint
- the index primarily composes, coordinates, or exports the unit rather than re-implementing all child details

Do not create `index.tsx` for every folder by habit.

Do not wrap a single component in a folder plus `index.tsx` without a real structural reason.

Do not let `index.tsx` become a supercomponent merely because it is the entrypoint. If the entrypoint accumulates child-specific state, effects, queries, or implementation details, move those responsibilities to the proper child files and ownership boundaries.

## Flutter Stateful Widget Pair

A `StatefulWidget` and its single matching `State<T>` class must remain together in the same file.

The matching `State<T>` class is part of the same widget implementation and does not count as a second widget for the one-widget-per-file rule.

Any additional Flutter widget declared in that file must be extracted into its own file.

Example:

```dart
class ProfilePage extends StatefulWidget {
  const ProfilePage({super.key});

  @override
  State<ProfilePage> createState() => _ProfilePageState();
}

class _ProfilePageState extends State<ProfilePage> {
  @override
  Widget build(BuildContext context) {
    return const SizedBox();
  }
}
```

This rule also applies to matching framework variants where the state class directly implements the lifecycle of exactly one widget, including:

- `StatefulWidget` + `State<T>`
- `ConsumerStatefulWidget` + `ConsumerState<T>`
- other equivalent stateful-widget/state pairs

Always verify that the state class is the single state class directly associated with that widget before applying this rule.

Controllers, notifiers, blocs, cubits, models, services, and additional widgets are not part of this exception and must follow their own file-structure rules.

## Narrow React Exception: Genuine Upstream shadcn/ui Files

A file may contain multiple React components only when all of the following are true:

1. The file was generated from or copied from the official upstream shadcn/ui registry.
2. Its multiple-component structure comes from that upstream file.
3. Keeping the structure is necessary to preserve straightforward upstream comparison, updates, or compatibility.
4. The file has not become a project-owned abstraction or feature component.

This exception does not apply merely because a file:

- lives under a `components/ui` directory
- imports shadcn/ui or Radix primitives
- uses shadcn styling conventions
- was inspired by shadcn/ui
- contains components that compose well together
- is small or internal

Project-owned wrappers, variants, composites, feature components, and extensions must use one component per file. When provenance is uncertain, treat the file as project-owned and split it. Do not expand the shadcn/ui exception for convenience.

Do not mechanically split a genuine, substantially upstream shadcn/ui file that satisfies every condition above.

## Required Final Verification

Before completing any task that creates or modifies React or Flutter UI code:

- [ ] Inspect every created or modified project-owned React/TSX and Flutter/Dart UI file.
- [ ] Count every React function, class, arrow function, or variable used as a component, including non-exported and nested components.
- [ ] Confirm that each project-owned React file contains exactly one React component.
- [ ] For project-owned TypeScript/TSX files, confirm filenames use lowercase `kebab-case` subjects with optional dot-role segments.
- [ ] Confirm each `index.ts` or `index.tsx` is a real logical-unit entrypoint rather than a habitual wrapper or dumping ground.
- [ ] Confirm that each project-owned Flutter file contains exactly one widget, except for its single matching state class when applicable.
- [ ] Confirm that every `StatefulWidget` and matching `State<T>` pair remains together in the same file.
- [ ] Confirm that no additional Flutter widget is declared beside that pair.
- [ ] For every file using the shadcn/ui exception, confirm all four upstream-provenance conditions above.
- [ ] Refactor every violation into one component or widget per file and update imports before running final checks.
- [ ] Re-scan the final diff after refactoring and confirm that zero violations remain.

Do not report the task as complete while any checklist item fails. A detected violation is required refactoring work, not an optional recommendation.

## Intent

Optimize for:

- readability
- grep/searchability
- predictable navigation
- responsibility-aligned file layout
- smaller diffs
- easier code review
- lower merge conflict risk
