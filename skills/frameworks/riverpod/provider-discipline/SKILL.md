---
name: riverpod-provider-discipline
description: Riverpod state management guidance focused on intentional provider usage, explicit state ownership, async state, dependency flow, performance, and testability.
---

# Riverpod Provider Discipline

Use Riverpod intentionally.

Riverpod is useful for shared state, dependency injection, async orchestration, caching, derived state, and business-relevant application state.

Do not automatically convert every piece of state or logic into a provider.

Riverpod should reduce complexity, not increase it.

## When to Use Riverpod

Use Riverpod for:

- shared state across widgets/screens
- business state
- async data fetching and caching
- repository/service dependency wiring
- derived/computed state
- cross-screen coordination
- state that benefits from testable dependency injection
- reusable stateful workflows

Avoid Riverpod for:

- temporary local UI toggles
- hover/focus state
- animation-only state
- local form field behavior
- widget-only ephemeral state
- one-off UI flags that never leave one widget subtree

Prefer local widget state when the state is truly local.

## Widget-Level Provider Discipline

Do not use Riverpod at widget level by default.

Widgets should usually:

- render UI
- consume already-owned state
- trigger actions
- coordinate simple interaction flow

Avoid creating providers just because a widget needs a boolean, controller, or tiny UI flag.

Examples that usually do not need providers:

```dart
bool isExpanded = false;
TabController tabController;
TextEditingController textController;
FocusNode focusNode;
```

Use providers only when state ownership, sharing, lifecycle, testing, caching, or recomputation benefits justify it.

## Provider Responsibilities

Providers should have clear ownership.

Good provider responsibilities:

- fetch and cache data
- expose business/application state
- derive state from other providers
- coordinate async mutations
- wire repositories/services
- expose reusable workflows

Avoid god providers that:

- fetch unrelated data
- mutate unrelated state
- own navigation
- format UI strings
- manage widget-only behavior
- mix API, UI, and routing concerns

## Provider Selection

Choose the simplest provider that matches the responsibility.

Use `Provider` for:

- immutable values
- dependency wiring
- computed/derived values

Use `Notifier` / `NotifierProvider` for:

- synchronous state with mutations
- business state that changes over time

Use `AsyncNotifier` / `AsyncNotifierProvider` for:

- async state with mutations
- async workflows that need methods
- loading/error/data state tied to business operations

Use `FutureProvider` for:

- simple one-shot async reads
- async values with no mutation methods
- lightweight derived async values

Use `StreamProvider` for:

- real-time streams
- websocket/auth state streams
- external stream sources

Do not force `AsyncNotifier` when `FutureProvider` is simpler and there are no mutations.

## Code Generation

Riverpod code generation is recommended when it improves maintainability.

Prefer `@riverpod` / `riverpod_generator` for:

- larger projects
- family providers
- async notifiers
- generated type safety
- consistency across a team
- reducing provider boilerplate

Do not introduce code generation blindly in small or legacy areas without considering project conventions.

If the project already uses Riverpod code generation, follow it consistently.

## `ref.watch`, `ref.read`, `ref.listen`, `select`

Use `ref.watch` when UI or provider state should react to changes.

Use `ref.read` for one-time reads, usually in event handlers or mutation methods.

Do not use `ref.read` inside `build` just to avoid rebuilds. It prevents proper reactivity.

Use `ref.listen` for side effects:

- snackbars
- dialogs
- navigation
- logging
- analytics

Keep side effects explicit and easy to trace.

Use `select` when only one field matters and rebuilds are costly or noisy.

Do not sprinkle `select` everywhere prematurely.

## Async State

Prefer `AsyncValue` patterns for async loading/error/data states.

Use `AsyncValue.guard` when it makes mutation error handling clearer.

Keep async ownership clear:

- fetching belongs in provider/repository boundaries
- rendering belongs in widgets
- retry/refetch behavior should be explicit
- do not duplicate loading state in multiple places

Avoid starting async work directly inside `build`.

## Repository Boundary

Keep data access separate from UI and provider orchestration.

Prefer:

```txt
UI widget
  -> provider / notifier
    -> repository
      -> API client / local storage
```

Repositories should own data access details.

Providers should coordinate state and workflows.

Widgets should not directly know API/client details unless the app is intentionally tiny.

## Family Providers

Use family providers when state depends on parameters such as:

- id
- filter
- query
- route parameter

Keep family parameters stable and equality-safe.

For complex parameters, use immutable value objects with proper equality.

Avoid passing large mutable objects as provider parameters.

## Lifecycle and Caching

Understand provider lifetime.

Use auto-dispose when state should disappear after no longer being watched.

Use keep-alive or caching only when there is a clear reason:

- expensive refetch
- app-level config
- session state
- reusable cached data

Clean up external resources with `ref.onDispose`.

Do not keep providers alive by default just because refetching is inconvenient.

## Performance

Optimize based on actual rebuild cost or observed noise.

Prefer:

- smaller widgets around provider watches
- derived providers for computed state
- `select` for specific fields
- stable provider parameters
- avoiding unnecessary provider churn

Avoid watching providers in a way that rebuilds large widget trees unnecessarily.

If a list item needs item-specific state, prefer extracting a focused child widget that watches only its own provider.

## Testing

Prefer provider tests for provider logic.

Prefer widget tests for UI behavior.

Use `ProviderContainer` or `ProviderScope` overrides to inject test dependencies.

Do not hide dependencies in globals when Riverpod can make them explicit and testable.

## Common Anti-Patterns

Avoid:

- creating providers for every widget field
- putting widget-only state in providers
- using `ref.read` in `build` to avoid rebuilds
- large god providers
- duplicated sources of truth
- hidden side effects inside provider reads
- business logic directly inside widgets
- navigation buried inside unrelated providers
- provider families with unstable mutable parameters
- caching everything forever
- adding code generation where the project does not use it and the benefit is unclear

## Review Checklist

When reviewing Riverpod code, ask:

- Does this state really need Riverpod?
- Who owns this state?
- Is the provider responsibility focused?
- Could local widget state be simpler?
- Is async loading/error/data handled consistently?
- Is there one clear source of truth?
- Are side effects explicit?
- Are provider parameters stable?
- Does this improve testability or just add ceremony?
