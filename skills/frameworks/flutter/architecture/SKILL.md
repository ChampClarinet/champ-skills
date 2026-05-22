---
name: flutter-architecture
description: Flutter app architecture guidance focused on separation of concerns, feature boundaries, and maintainable layers.
---

# Flutter Architecture

Use this skill when designing, reviewing, or refactoring Flutter app structure.

## Core Principles

- Separate UI, logic, and data concerns.
- Prefer predictable feature boundaries.
- Keep widgets focused on rendering and interaction.
- Keep business logic out of widgets when it grows beyond simple UI behavior.
- Prefer boring, explicit architecture over clever abstractions.
- Add layers only when the complexity justifies them.

Flutter's official architecture guide emphasizes separation of concerns and splitting apps into UI and data layers, with additional components/layers when needed.

## Layer Guidance

Prefer these responsibilities:

- UI layer:
  - widgets
  - screens/pages
  - presentation state
  - user interaction wiring

- Logic/application layer:
  - use cases
  - orchestration
  - app-specific workflows
  - reusable business operations

- Data layer:
  - repositories
  - API clients
  - DTOs/models
  - local storage
  - remote/local data coordination

Do not create a domain/use-case layer just to look clean. Use it when logic is complex, reused, or needs isolation.

## Feature Boundaries

Prefer feature-first organization when it improves navigation and ownership.

A feature may contain:

```txt
features/
  wine/
    data/
    providers/
    widgets/
    screens/
```

Avoid dumping everything into global folders like:

```txt
widgets/
services/
utils/
```

unless the code is truly shared across multiple features.

## Widget Discipline

- Keep widgets small enough to understand.
- Extract widgets for readability, not just to reduce line count.
- Avoid god widgets that own rendering, fetching, mutation, validation, and navigation at once.
- Prefer explicit dependencies over hidden global behavior.

## Review Checklist

When reviewing Flutter architecture, check:

- Is the responsibility in the right layer?
- Is the feature boundary clear?
- Is this abstraction solving a real repeated problem?
- Can this be simpler?
- Will future changes be easy to locate?
- Does the structure match how the app is actually used?
