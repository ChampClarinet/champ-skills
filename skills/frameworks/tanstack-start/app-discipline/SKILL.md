---
name: tanstack-start-app-discipline
description: TanStack Start guidance focused on routing, server functions, server routes, SSR, Vite integration, and maintainable full-stack React architecture.
---

# TanStack Start App Discipline

Use TanStack Start as a full-stack React framework powered by TanStack Router and Vite.

TanStack Start should keep routing type-safe, server/client boundaries explicit, and full-stack behavior easy to trace.

Do not treat TanStack Start as just Vite with extra files, and do not treat it as Next.js with different names.

## Core Principles

- Prefer explicit route ownership.
- Keep routing behavior easy to trace.
- Keep server/client boundaries intentional.
- Use server functions for server-only work.
- Use server routes for intentional API endpoints.
- Keep Vite configuration simple and justified.
- Prefer framework-native patterns before custom orchestration.
- Keep type safety readable and maintainable.

## Framework Role

TanStack Start provides:

- full-document SSR
- streaming
- server functions
- server routes / API routes
- middleware and context
- full-stack bundling
- Vite-powered development/build tooling
- TanStack Router-powered routing

Use these capabilities intentionally.

If the app does not need full-stack features, SSR, server routes, or server functions, consider whether TanStack Router + Vite is enough.

## Route Organization

Prefer route structure that mirrors product/domain navigation.

Keep route files focused on route ownership:

- route component
- route loader
- route-level validation
- route-level server interactions
- route-specific error/loading behavior

Avoid hiding route-critical behavior in unrelated utility files.

## Routing Discipline

Use TanStack Router strengths intentionally:

- type-safe routes
- nested routes
- route loaders
- search params
- route context
- explicit route ownership

Avoid:

- magic route strings scattered everywhere
- duplicated route constants
- hidden navigation side effects
- route loaders that become business workflow dumping grounds

## Server Functions

Use server functions for logic that must run on the server:

- database access
- secrets/environment variables
- filesystem access
- authenticated server-side operations
- server-only integrations

Server functions are type-safe RPC-style server capabilities and can be called from components, loaders, hooks, and other app code.

Keep server functions focused.

Avoid turning server functions into a hidden service layer with unclear ownership.

Do not expose secrets to the client.

## Server Function Security

Treat server functions as same-origin server endpoints.

Do not assume they are public cross-origin APIs.

Use server routes/API routes for endpoints intentionally designed as public or cross-origin APIs.

Use CSRF protection/middleware according to project setup when server functions are enabled.

## Server Routes / API Routes

Use server routes when the app needs explicit backend endpoints.

Good use cases:

- public API endpoints
- webhooks
- cross-origin integration points
- file uploads/downloads
- endpoints consumed outside the app shell

Avoid using server routes when a focused server function is clearer and only used by the app itself.

## SSR and Streaming

Use SSR and streaming intentionally.

Prefer SSR for:

- initial page performance
- SEO-sensitive pages
- authenticated server-derived data
- full-stack route ownership

Avoid adding SSR complexity when a simple client-only route is sufficient.

Keep loading and streaming boundaries understandable.

## Data Ownership

Prefer route-level or domain-level data ownership.

Avoid duplicating the same data fetching across:

- route loaders
- server functions
- client hooks
- component effects

If TanStack Query is used, keep cache ownership and invalidation explicit.

Do not create multiple sources of truth for the same server state.

## Client State

Use client state for:

- local UI interaction
- ephemeral UI state
- form interaction
- browser-only behavior

Do not push server-owned data into global client state unless there is a clear reason.

## Vite Boundary

TanStack Start uses Vite, but Vite config should remain tooling-focused.

Use Vite config for:

- TanStack Start plugin
- React plugin
- path aliases
- deployment/runtime plugins
- build/dev tooling

Do not put application architecture decisions into Vite config.

## Deployment Discipline

Keep deployment behavior explicit.

Understand the selected runtime/hosting target.

When using Nitro or hosting adapters, keep the build/start behavior documented.

Do not assume dev server behavior matches production.

Test production builds when changing server functions, server routes, SSR behavior, or deployment config.

## SPA Mode

Use SPA mode only when the deployment/runtime intentionally does not use full server rendering.

If server functions or server routes are still needed in SPA mode, make routing/rewrites explicit.

Do not accidentally break server function or API route access with catch-all SPA rewrites.

## Environment Variables

Keep server-only values server-only.

Do not expose secrets to client code.

Use server functions/server routes for secret-backed operations.

Avoid client-side environment variable leaks.

## Error Boundaries

Keep error ownership close to the route or domain that can fail.

Prefer route-specific error handling when failures are route-specific.

Avoid one giant generic error boundary hiding unrelated failure modes.

## Middleware and Context

Use middleware and request context intentionally.

Good use cases:

- auth/session context
- request metadata
- tracing/logging
- security checks
- shared server-side dependencies

Avoid middleware chains that hide business logic or make request flow hard to trace.

## TypeScript

Use TypeScript-first patterns.

Prefer end-to-end type safety when it improves correctness and maintainability.

Avoid type gymnastics that make route/server behavior harder to understand.

## Review Checklist

When reviewing TanStack Start code, ask:

- Is this using TanStack Start features intentionally?
- Is route ownership clear?
- Is server/client behavior easy to trace?
- Should this be a server function or a server route?
- Are secrets kept server-side?
- Is data fetched in one clear place?
- Is cache invalidation explicit?
- Is Vite config still tooling-focused?
- Is deployment behavior understood?
- Can this be simpler?
