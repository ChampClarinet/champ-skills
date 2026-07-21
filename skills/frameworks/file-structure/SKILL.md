---
name: file-structure
description: Mandatory file organization rules for maintainable component and class structure.
---

# File Structure

Use one primary class or component per file.

## Non-Negotiable Rules

- One Flutter widget class per file.
- Exactly one project-owned React component per file.
- One domain, service, or model class per file.
- File names must match the primary class or component name.
- Never group multiple project-owned React components in one file, even when they are small, private, closely related, used only once, or compose a single screen.
- Extract every additional project-owned React component into its own file and import it.
- Do not treat non-exported, nested, helper, local, or subcomponents as exceptions. If a function or variable is used as a React component, it is a component for this rule.
- Avoid grouping unrelated classes or components in the same file.
- Avoid "misc", "utils", or "components" files becoming dumping grounds.

Terms such as "prefer", "when practical", file size, convenience, locality, or reduced import count must not weaken these rules. For project-owned React code, one component per file is a completion requirement.

Non-component helpers, hooks, types, constants, and data may remain alongside the file's single component when they are tightly coupled to it. They must not render JSX or be used as React components.

## Flutter Exception

A Flutter `StatefulWidget` and its matching `State` class may live in the same file.

Example:

```dart
class ProfilePage extends StatefulWidget {}

class _ProfilePageState extends State<ProfilePage> {}
```

This also applies to inherited StatefulWidget variants.

Always verify whether the widget actually inherits from `StatefulWidget` before applying this exception.

Example:

```dart
class ProfilePage extends ConsumerStatefulWidget {}

class _ProfilePageState extends ConsumerState<ProfilePage> {}
```

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

Before completing any task that creates or modifies React code:

- [ ] Inspect every created or modified project-owned React/TSX file.
- [ ] Count every function, class, arrow function, or variable used as a React component, including non-exported and nested components.
- [ ] Confirm that each project-owned file contains exactly one React component.
- [ ] For every file using the shadcn/ui exception, confirm all four upstream-provenance conditions above.
- [ ] Refactor every violation into one component per file and update its imports before running final checks.
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
