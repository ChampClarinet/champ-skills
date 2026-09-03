---
name: bun-monorepo
description: Conventions for Bun workspace monorepos containing applications, independently deployable services, and shared packages, including dependency boundaries, scripts, builds, and Vercel deployments. Use when creating, reviewing, migrating, or restructuring Bun monorepos.
---

# Bun Monorepo

Use Bun workspaces as the default lightweight monorepo foundation when the repository uses Bun. Do not introduce Turborepo, Nx, or another orchestration layer unless the repository has a demonstrated need for it. Start simple.

## Recommended semantics

A useful convention is:

```text
apps/
services/
packages/
```

Meaning:

- `apps/`: user-facing products; may contain frontend plus product backend; independently deployable.
- `services/`: backend-only runtime services; independently deployable.
- `packages/`: non-deployable shared libraries, contracts, tooling, or configuration.

These names are conventions, not Bun requirements. Do not force this layout onto an existing project when another clear structure is already established.

## Workspaces

A typical root configuration can include:

```json
{
  "private": true,
  "workspaces": ["apps/*", "services/*", "packages/*"]
}
```

Each workspace must declare the dependencies it actually uses. Do not rely on accidental dependency availability from the repository root. Prefer dependency isolation that exposes undeclared dependency usage early.

## Runtime boundaries

Workspace boundaries and runtime boundaries are not the same thing.

A package being importable through Bun workspaces does not mean importing it is architecturally valid.

For independently deployed services, communicate through the published network/service contract. Do not import another service's database, repositories, route implementation, or private business logic even when both services live in the same repository.

Shared repository does not mean shared runtime.

## Shared packages

Use `packages/` only for code that is legitimately shared.

Good candidates include:

- protocol primitives,
- generated API clients,
- reusable transport schemas,
- framework-independent utilities,
- lint/TypeScript configuration,
- design-system packages where justified.

Bad candidates include:

- another service's repositories,
- another service's private database schema,
- service-private business logic,
- ORM models used to bypass a service API,
- miscellaneous code moved to `shared` merely because two files need it.

Avoid creating a shared dumping ground.

## Contracts

For runtime services, prefer published contracts over implementation imports.

TypeScript clients may use generated or framework-native typed clients. Cross-repository consumers must have a portable mechanism such as OpenAPI, a generated SDK/package, or another versioned protocol contract.

Do not design a service API that can only be consumed by cloning its source repository.

## Root scripts

Provide useful root-level orchestration for common repository checks, such as dev, lint, typecheck, test, build, and an aggregate check where useful.

Root commands should either run the appropriate command across relevant workspaces or clearly document workspace-specific alternatives.

Never hide failures using `|| true`. A successful root verification should mean the repository is actually healthy.

## Workspace scripts

Each deployable should own its relevant scripts, commonly:

- `dev`
- `build`
- `start`
- `lint`
- `typecheck`
- `test`

A workspace should not require unrelated deployables to build just to run locally unless there is a real dependency.

## Bun-first

Prefer Bun tooling when supported:

- `bun install`
- `bun run`
- `bun test`
- Bun workspace resolution

Do not mix package managers without a documented reason. Keep one canonical lockfile and respect the Bun version declared by the repository.

## Dependency changes

When adding a dependency:

1. identify which workspace actually uses it,
2. add it there,
3. do not default to the repository root.

Root dependencies should primarily support repository-wide tooling.

## TypeScript

Shared TypeScript configuration may live in a package or root configuration.

Do not allow path aliases to create hidden cross-service coupling. Aliases improve ergonomics; they do not authorize architecture violations.

Always verify typechecking from actual consumer workspaces.

## Vercel

One Git repository may map to multiple Vercel Projects. Each independently deployable workspace can use its own Root Directory.

For example:

```text
apps/product
    -> Vercel Project: product

services/core
    -> Vercel Project: core

services/identity
    -> Vercel Project: identity
```

Each Vercel Project should own its deployment configuration, environment variables, domains, and build lifecycle.

Do not assume one repository means one deployment. Conversely, do not create extra Vercel projects when components intentionally deploy as one unit. A Next.js frontend with an embedded product API can remain one Vercel Project.

## Environment variables

Keep secrets scoped to the deployable that requires them. Do not place every service secret into a common root environment file merely because the repository is shared.

Prefer service-specific ignored local env files and service-specific deployment-platform env configuration.

Public browser variables must be explicitly safe for public exposure. Never expose service credentials or private keys through browser-prefixed variables.

## Deployment independence

An independently deployable service should be able to install, typecheck, test, build, and deploy without depending on another service's private implementation.

Shared packages may be intentional build dependencies. Network-service dependencies should remain network dependencies.

## Docker

If Docker is used, prefer workspace-specific build contexts or well-defined monorepo-aware builds.

Do not copy unrelated secrets, archived/reference trees, local caches, or generated development artifacts into production images.

## Generated files

Generated build output should not normally be committed, including `.next/`, coverage output, build caches, and local typecheck artifacts.

Generated source that forms part of a published contract may be committed only when the project intentionally chooses that workflow.

## Legacy/reference trees

If the repository contains archived code such as `.old/`:

- exclude it from active lint/typecheck/build/test tooling,
- never import it into current work,
- do not delete or rewrite it unless explicitly instructed.

## When to add Turborepo

Do not add Turborepo merely because the repository is a monorepo.

Consider it when actual needs appear, such as expensive repeated builds, complex task dependency graphs, remote caching, or many workspaces with significant orchestration cost. Document why the additional layer is needed.

## Guardrails

Before introducing a cross-workspace import, ask:

1. Is this a shared-library dependency or a runtime-service dependency?
2. Who owns this code?
3. Would the import still make sense if the service lived in another repository?
4. Does this bypass an API, security, or domain boundary?

If the import bypasses a runtime boundary, use the service contract instead.

## Before finishing

Run the repository's relevant install/workspace resolution, lint, typecheck, tests, and builds. Also verify each independently deployable workspace can pass its own checks.
