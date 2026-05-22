---
name: go-router-routing-discipline
description: Guidance for organizing routes, redirects, navigation flow, and go_router usage boundaries.
---

# go_router Routing Discipline

Use go_router to keep navigation declarative, centralized, and predictable.

go_router is most valuable for:

- URL-aware navigation
- deep linking
- nested routing
- redirect handling
- shell navigation
- centralized route configuration

## Route Organization

Prefer centralized route ownership.

Example:

```txt
router/
  app_router.dart
  route_names.dart
  routes/
```

Avoid scattering route definitions across unrelated files unless the app scale justifies modularization.

## Route Naming

Prefer explicit route names and paths.

Good:

```dart
name: RouteNames.profile
path: '/profile'
```

Avoid:

```dart
'/p'
```

unless intentionally optimized for public URLs.

## Navigation Discipline

Prefer navigation flows that are easy to trace.

Avoid:

- hidden redirects
- implicit navigation side effects
- deeply nested redirect chains
- navigation triggered indirectly by unrelated state changes

## Redirect Logic

Keep redirect logic:

- predictable
- centralized
- easy to reason about

Avoid putting large business workflows inside redirect callbacks.

Redirects should preferably answer:

```txt
Can this route be entered?
If not, where should the user go?
```

## Shell Routes

Use shell routes when:

- multiple screens share navigation structure
- tabs share layout
- persistent navigation UI is needed

Avoid over-nesting shell routes without clear UX benefit.

## Deep Link Discipline

Prefer routes that:

- can be reconstructed from URL state
- behave consistently from direct links
- avoid hidden navigation assumptions

## Widget Integration

Widgets should not own routing architecture.

Prefer:

- centralized route definitions
- route constants
- explicit navigation APIs

Avoid:

- hardcoded magic route strings everywhere
- duplicated route paths
- deeply coupled navigation logic inside widgets

## Architecture Philosophy

Navigation should be easy to trace mentally.

Prefer:

- explicitness
- predictability
- centralized ownership
- maintainable route structure

over routing cleverness.
