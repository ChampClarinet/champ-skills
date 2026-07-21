---
name: file-structure
description: Mandatory file organization rules for maintainable component and class structure.
---

# File Structure

Use one primary class or component per file.

## Non-Negotiable Rules

- Exactly one project-owned Flutter widget per file.
- Exactly one project-owned React component per file.
- One domain, service, or model class per file.
- File names must match the primary class or component name.
- Never group multiple project-owned React components in one file, even when they are small, private, closely related, used only once, or compose a single screen.
- Extract every additional project-owned React component into its own file and import it.
- Do not treat non-exported, nested, helper, local, or subcomponents as exceptions. If a function or variable is used as a React component, it is a component for this rule.
- Do not evade the React rule by converting a component into a `renderX`, `getX`, JSX-returning callback, or component factory. A substantial UI section with its own responsibility must be extracted into its own component file.
- Avoid grouping unrelated classes or components in the same file.
- Avoid "misc", "utils", or "components" files becoming dumping grounds.

Terms such as "prefer", "when practical", file size, convenience, locality, or reduced import count must not weaken these rules. For project-owned React code, one component per file is a completion requirement.

Non-component helpers, hooks, types, constants, and data may remain alongside the file's single component when they are tightly coupled to it. They must not render JSX or be used as React components.

A route, page, or layout may remain the single primary React component in its own file. Do not create a redundant pass-through wrapper merely to satisfy this rule.

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
- smaller diffs
- easier code review
- lower merge conflict risk
