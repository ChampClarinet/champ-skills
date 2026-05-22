---
name: file-structure
description: File organization rules for maintainable component and class structure.
---

# File Structure

Prefer one primary class or component per file.

## Rules

- One Flutter widget class per file.
- One React component per file.
- One domain, service, or model class per file.
- File names should match the primary class or component name.
- Avoid grouping unrelated classes or components in the same file.
- Avoid "misc", "utils", or "components" files becoming dumping grounds.

## Exceptions

Flutter `StatefulWidget` and its matching `State` class may live in the same file.

Example:

```dart
class ProfilePage extends StatefulWidget {}

class _ProfilePageState extends State<ProfilePage> {}
```

Also applies to inherited StatefulWidget variants.

Always verify whether the widget actually inherits from StatefulWidget before applying this exception.

Example:

```dart
class ProfilePage extends ConsumerStatefulWidget {}

class _ProfilePageState extends ConsumerState<ProfilePage> {}
```
