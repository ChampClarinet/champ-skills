---
name: elysiajs
description: Opinionated conventions for building Elysia APIs, including standalone services, Next.js integration, Eden, OpenAPI, validation, composition, testing, and service boundaries. Use when creating, reviewing, or restructuring Elysia APIs or Elysia-backed Next.js APIs.
---

# ElysiaJS

Use Elysia as the standard API framework when the project has selected Elysia. Prefer Elysia-native patterns over custom abstractions, and follow current official Elysia guidance when framework behavior or syntax is version-sensitive.

## Core principles

- Keep the Elysia app as the canonical API definition.
- Use runtime schemas for validation.
- Derive TypeScript types from the API/schema whenever practical.
- Export the Elysia application type for Eden consumers.
- Use OpenAPI as the portable, language-neutral external contract.
- Use Eden for TypeScript-native consumer ergonomics.
- Keep Elysia and Eden versions compatible across producer and consumer.
- Prefer explicit service boundaries over convenient implementation imports.

Do not duplicate the same contract as a TypeScript interface, validation schema, OpenAPI schema, and client DTO unless there is a documented reason. One canonical API definition should drive as much of the contract as possible.

## Next.js + Elysia

When an API belongs to a product that already has a Next.js frontend, prefer embedding Elysia into the Next.js application instead of creating a separate backend deployment without a clear reason.

Recommended shape:

```text
app/
└── api/
    └── [[...slugs]]/
        └── route.ts

src/
└── server/
    └── api/
        └── app.ts
```

The Next.js route should remain a thin adapter around `api.fetch`. Export only the HTTP methods the API intends to support. The real API composition belongs in the Elysia application.

Keep the Elysia app server-only. Do not place business or domain logic in the Next.js catch-all adapter.

## Standalone services

When a backend service has no paired frontend, run Elysia as a standalone deployable service. Examples include shared domain services, identity services, integration services, and internal platform APIs.

A standalone service should follow the same contract conventions:

- Elysia
- runtime schemas
- OpenAPI
- Eden-compatible exported application type
- consistent errors
- health endpoint
- environment validation

Do not create a dummy Next.js application merely to host an API.

## Composition

Compose APIs through Elysia plugins/routes rather than one giant application file. Prefer feature/domain ownership and keep composition explicit enough that ownership remains obvious.

Do not create generic CRUD abstractions that hide domain behavior.

## Schemas

Prefer reusable named schemas/models when a shape represents a stable API concept.

Use runtime schemas for request bodies, parameters, query strings, and important response contracts. Schemas should improve runtime validation, API discoverability, OpenAPI output, and type inference.

Do not expose database rows as public API contracts merely because their shapes are convenient. Persistence models and transport contracts are different concerns.

## Eden

Use Eden for TypeScript consumers when it improves developer experience.

Export the server application type, for example:

```ts
export type ApiApp = typeof api;
```

Important:

- use strict TypeScript,
- align Elysia/Eden versions,
- verify consumer typecheck,
- ensure path aliases resolve consistently.

In monorepos, do not assume server type inference is portable merely because workspaces compile individually. Typecheck from the actual consumer workspace too.

Eden is a transport/client convenience. It does not grant permission to import service implementation code across runtime service boundaries. Independently deployed services must still communicate over their network boundary.

## OpenAPI

Expose OpenAPI for development and service integration. Prefer disabling interactive documentation in production unless the project explicitly requires public API documentation.

OpenAPI is the portable external contract for non-TypeScript consumers, cross-repository consumers, generated clients, and integration tooling.

Do not make external consumers depend permanently on monorepo-only TypeScript imports.

## Authentication and authorization

Authentication plugins may enrich request context, but keep these concepts distinct:

- user authentication,
- service authentication,
- authorization,
- domain validation.

A valid identity does not imply permission. A valid service credential does not imply permission. Receiving services must enforce their own authorization and invariants.

## Errors

Use stable machine-readable error identifiers where useful and human-readable messages separately.

Avoid leaking database errors, SQL, stack traces, secret/config values, or internal authorization details.

Centralize truly cross-cutting error behavior while allowing domains to own domain-specific errors.

## Server-only boundaries

Privileged credentials must stay server-side. Browser code must never receive database owner/service credentials, service private keys, privileged Supabase keys, or infrastructure secrets.

Use `server-only` or equivalent safeguards where appropriate.

## Testing

Test at the Elysia application boundary where practical. Prefer tests for status codes, validation, authentication, authorization, error contracts, and important domain invariants.

For embedded Next.js APIs, most API behavior should be testable without repeatedly testing the thin Next.js adapter.

## Avoid

Do not:

- put business logic inside `route.ts`,
- duplicate route definitions outside Elysia,
- import another independently deployed service's implementation,
- rely on client-only validation,
- expose privileged environment variables to the browser,
- create giant shared DTO packages,
- bypass service boundaries because code shares a repository,
- introduce unnecessary abstractions over Elysia.

## Before finishing

Run the project's relevant lint, typecheck, tests, and build commands. For Eden/monorepo work, verify both producer and consumer typechecks.
