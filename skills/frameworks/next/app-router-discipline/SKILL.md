---
name: next-app-router-discipline
description: Champ's Next.js App Router defaults for server/client boundaries, route ownership, data flow, caching, and framework-native behavior. Use when implementing or reviewing Next.js App Router code.
---

# Next.js App Router Discipline

Prefer framework-native App Router behavior over custom client orchestration.

Repository-local explicit conventions override these defaults.

## Server and client boundaries

Prefer Server Components by default.

Add `"use client"` only when the owned behavior requires client runtime capabilities such as interaction state, browser APIs, client-only hooks, animation, or imperative libraries.

Keep client boundaries as narrow as the owned interactive workflow permits. Do not make a page or layout client-side merely because one descendant needs interaction.

Do not move state upward solely to avoid a client boundary. Compose with `ownership-boundaries` and `react-component-ownership` to place the boundary around the actual owner.

## Data ownership

Prefer server-side ownership for initial, authenticated, database-backed, route-driven, or SEO-relevant data when practical.

Avoid duplicating the same server state into client fetching or global client stores without a real lifecycle or interaction requirement.

Keep async ownership close to the route or domain boundary that owns it. Avoid client fetch waterfalls and duplicated loading orchestration when server composition can express the flow directly.

Use `loading.tsx`, Suspense, route boundaries, and framework-native async rendering when they match the ownership boundary.

## Effects and mutations

Do not use client effects for work that belongs to server rendering, derived render state, routing state, or explicit user events.

Use Server Actions when server-owned mutations or form workflows benefit from them, but do not turn them into an opaque RPC layer. Keep authorization, side effects, and ownership traceable.

## Routing and layouts

Keep route structure aligned with product or domain ownership.

Use layouts for genuinely shared route structure and persistent shells. Do not turn layouts into dumping grounds for unrelated business logic.

Keep errors close to the route or workflow boundary that can meaningfully recover or explain the failure.

Use framework-native metadata for route-specific SEO rather than scattering metadata behavior through unrelated components.

## Cache and revalidation

Make cache behavior intentional.

Do not disable caching globally because the active rendering or invalidation model is unclear.

When correctness depends on freshness, identify the owner of invalidation/revalidation and verify the active Next.js version's semantics rather than relying on remembered defaults.

## PWA and service workers

Add PWA behavior only when the product requires installability, offline behavior, push, background behavior, or explicit caching.

A service worker must have clear ownership for:

- what is cached
- update and invalidation behavior
- stale assets
- offline fallback
- failed mutations or retry behavior
- how users receive updated application code

Do not imply offline support when only static assets are cached.

Notification permission prompts should be contextual and user-triggered rather than automatic on first load.

## Composition

- `ownership-boundaries` owns general state and behavior ownership.
- `react-component-ownership` maps ownership into React component boundaries.
- `file-structure` owns project file organization and naming.
- `layout-system` owns structural layout and responsive behavior.
- `tooling-feedback` owns framework diagnostics on touched code.

This skill should contain Next.js-specific decisions, not duplicate those policies.

## Verification

For touched App Router behavior, verify:

- each client boundary is required by client-owned behavior
- server-owned data is not duplicated into client state without reason
- loading/error/mutation ownership is traceable
- cache and revalidation semantics match the active Next.js version
- route and layout boundaries reflect meaningful ownership
- PWA/service-worker behavior has explicit cache/update/offline semantics when present
