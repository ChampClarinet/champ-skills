---
name: next-app-router-discipline
description: Next.js App Router guidance focused on server/client boundaries, rendering behavior, routing structure, data ownership, and maintainable React architecture.
---

# Next.js App Router Discipline

Use Next.js App Router to keep rendering, routing, and data flow predictable and maintainable.

Prefer framework-native patterns before introducing custom orchestration.

## Core Principles

- Prefer Server Components by default.
- Keep client boundaries intentional.
- Prefer server-side data ownership when practical.
- Keep rendering behavior explicit.
- Avoid unnecessary client-side effects and state duplication.
- Prefer framework-native data flow over custom client orchestration.

## Server vs Client Components

Prefer Server Components unless client interactivity is required.

Good reasons for `"use client"`:

- browser APIs
- local interactive UI state
- animations
- imperative UI libraries
- client-side event handling
- hooks that require the client runtime

Do not add `"use client"` automatically.

Avoid pushing large trees into client rendering unnecessarily.

## Client Boundary Discipline

Keep client boundaries small and intentional.

Prefer:

```txt
Server Page
  -> Small Client Component
```

over:

```txt
Entire page = client component
```

Avoid turning layouts/pages client-side unless required.

## Routing Structure

Prefer predictable route ownership.

Example:

```txt
app/
  dashboard/
    page.tsx
    loading.tsx
    error.tsx
```

Keep route structure aligned with product/domain structure.

Avoid deeply confusing route nesting without UX justification.

## Data Fetching

Prefer server-side data fetching when practical.

Prefer:

- Server Components
- route handlers
- server actions when appropriate
- framework-native caching/revalidation

Avoid unnecessary client-side fetching for initial page data.

Do not duplicate the same fetch across server and client unnecessarily.

## Async Discipline

Prefer async ownership close to the route or domain boundary.

Avoid:

- cascading client fetch waterfalls
- deeply nested loading orchestration
- duplicated loading states
- fetching inside many unrelated child components

Prefer predictable loading boundaries using:

- `loading.tsx`
- Suspense
- route-level async ownership

## State Ownership

Keep state ownership clear.

Use client state for:

- local UI interaction
- ephemeral UI behavior
- client-only workflows

Prefer server ownership for:

- initial data
- authenticated data
- database-backed state
- SEO-relevant content
- route-driven data

Avoid duplicating server state unnecessarily into client global stores.

## Effects Discipline

Avoid unnecessary `useEffect`.

Do not use effects for:

- initial server data loading
- derived values
- framework-native routing state
- things that can be rendered directly

Prefer:

- async Server Components
- server actions
- explicit event handlers
- derived render values

over effect-heavy orchestration.

## Server Actions

Use server actions intentionally.

Good use cases:

- forms
- mutations
- authenticated operations
- simple server-side workflows

Avoid turning server actions into hidden RPC systems.

Keep ownership and side effects understandable.

## Caching and Revalidation

Prefer explicit cache behavior.

Understand:

- static rendering
- dynamic rendering
- revalidation
- cache invalidation

Do not disable caching globally out of confusion.

Avoid cargo-cult cache configuration.

## Layout Discipline

Use layouts for:

- shared navigation
- shared UI structure
- route grouping
- persistent shells

Avoid putting unrelated business logic into layouts.

## Error Handling

Use:

- `error.tsx`
- route-level boundaries
- predictable fallback behavior

Keep error ownership close to the failing boundary.

Avoid giant global catch-all UX for unrelated failures.

## SEO / Metadata

Prefer framework-native metadata handling.

Use metadata intentionally for:

- titles
- descriptions
- OG tags
- route-specific SEO

Avoid scattering SEO logic across unrelated components.

## Performance

Optimize based on actual bottlenecks.

Prefer:

- Server Components
- streaming/Suspense when useful
- smaller client bundles
- intentional dynamic imports
- route-level ownership

Avoid premature optimization complexity.

## Tailwind / shadcn / Radix

Current preferred UI stack:

- Tailwind CSS
- shadcn/ui
- Radix UI

Keep styling and component boundaries maintainable.

Do not couple routing/rendering logic tightly with UI library internals.

## Review Checklist

When reviewing Next.js App Router code, ask:

- Does this really need `"use client"`?
- Is data owned at the correct boundary?
- Is fetching duplicated unnecessarily?
- Is rendering behavior predictable?
- Is routing structure understandable?
- Can this be simpler?
- Is state duplicated between server and client?
- Is async behavior easy to trace?
- Would another developer understand this quickly?

## PWA Discipline

Use PWA features intentionally when the product needs installability, offline behavior, push notifications, or app-like UX.

Core PWA areas:

- web app manifest
- service worker
- offline fallback
- installability
- push notifications when needed
- caching strategy
- local testing
- security

Prefer Next.js App Router PWA conventions when available.

Keep PWA behavior explicit and testable.

Do not add service workers casually. Service workers can create confusing cache bugs if ownership and update behavior are unclear.

## Manifest

Use a web app manifest when the app should be installable or app-like.

Keep manifest values intentional:

- name
- short_name
- icons
- start_url
- display
- theme_color
- background_color

Do not leave placeholder metadata in production.

## Service Worker

Add a service worker only when the app has clear offline, caching, push, or background behavior requirements.

When using a service worker, define:

- what is cached
- when cache updates
- offline fallback behavior
- how stale assets are handled
- how users receive updates

Avoid mysterious service worker behavior that makes production bugs hard to reproduce.

## Offline Behavior

If offline support exists, design it explicitly.

Prefer:

- clear offline fallback UI
- predictable cached pages/assets
- safe handling of failed mutations
- user-visible retry behavior

Do not imply offline support if only static assets are cached.

## Push Notifications

Use push notifications only when product value is clear.

Keep permission prompts intentional and user-triggered.

Do not ask for notification permission on first page load without context.

## PWA Testing

Test PWA behavior locally and in production-like builds.

Verify:

- manifest loads correctly
- service worker registers correctly
- install prompt works where supported
- offline fallback behaves correctly
- cache update behavior is understandable
- no secrets are exposed to client-side code
