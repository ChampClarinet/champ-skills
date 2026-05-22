---
name: vite-project-discipline
description: Vite project guidance focused on simple tooling, explicit config, environment variables, aliases, build behavior, and maintainable frontend workflow.
---

# Vite Project Discipline

Use Vite as fast, explicit frontend tooling.

Vite should keep development fast and configuration understandable.

Do not turn Vite config into a hidden framework.

## Core Principles

- Prefer simple Vite config.
- Prefer explicit project conventions.
- Prefer fast feedback loops.
- Keep environment handling clear.
- Keep aliases predictable.
- Add plugins only when they solve a real problem.
- Avoid build-system cleverness unless the project actually needs it.

## Project Role

Treat Vite primarily as:

- dev server
- bundler/build pipeline
- frontend tooling layer
- plugin integration point

Do not use Vite config as a dumping ground for application architecture.

Application architecture belongs in app code, modules, routing, and framework-specific layers.

## Config Discipline

Keep `vite.config.ts` readable.

Good config usually includes only:

- framework plugin
- aliases
- environment-specific build/dev settings
- required test/tooling integration
- clearly justified plugins

Avoid:

- large custom logic
- hidden environment branching
- unrelated app constants
- complicated plugin chains without clear reason

## Environment Variables

Use `import.meta.env` for Vite environment access.

Only variables prefixed with `VITE_` are exposed to client-side code.

Do not put secrets in `VITE_` variables.

Use `VITE_` only for values safe to ship to the browser, such as:

```txt
VITE_API_BASE_URL
VITE_APP_ENV
VITE_PUBLIC_ANALYTICS_ID
```

Avoid:

```txt
VITE_DATABASE_PASSWORD
VITE_PRIVATE_API_KEY
VITE_SERVER_SECRET
```

If a value is secret, keep it server-side.

## Mode Discipline

Use Vite modes intentionally.

Prefer clear environment files:

```txt
.env
.env.local
.env.development
.env.production
```

Avoid too many near-duplicate environment files unless the deployment workflow requires them.

Do not rely on hidden local environment assumptions.

## Alias Discipline

Use aliases to improve readability, not to hide project structure.

Common pattern:

```ts
resolve: {
  alias: {
    "@": path.resolve(__dirname, "./src"),
  },
}
```

If using TypeScript path aliases, keep Vite aliases and `tsconfig` paths aligned.

Avoid many clever aliases that make imports harder to trace.

## Plugin Discipline

Add plugins only when they have a clear purpose.

Good reasons:

- React support
- SVG/component imports
- PWA support
- bundle analysis
- testing integration
- legacy browser support when required

Avoid plugin accumulation because examples online include them.

If a plugin is added, its purpose should be obvious from config or documentation.

## Build Discipline

Keep production build behavior predictable.

Prefer:

- explicit build scripts
- clear output directory
- readable asset handling
- CI build verification
- previewing production builds when needed

Do not assume dev behavior equals production behavior.

Use production build/preview when investigating build-only issues.

## Asset Handling

Use Vite asset handling conventions unless the project has a specific reason not to.

Keep static assets organized and easy to trace.

Avoid mixing public/static/runtime assets without clear ownership.

## Dev Server Discipline

Keep dev server configuration minimal.

Only customize:

- host/port
- proxy
- HTTPS
- HMR
- filesystem access

when the project actually needs it.

Avoid dev-only behavior that hides production problems.

## Proxy Discipline

Use dev proxy for local development convenience.

Do not confuse dev proxy behavior with production API architecture.

Production API routing should be explicit in deployment/backend configuration.

## Testing Integration

If the project uses Vitest, keep test config aligned with Vite where practical.

Avoid duplicating aliases and environment assumptions across tooling.

## Performance

Vite is already optimized for fast development.

Optimize config only when there is an observed issue:

- slow startup
- slow HMR
- large dependency pre-bundling cost
- production bundle concerns

Avoid premature optimizeDeps/plugin tuning without evidence.

## Framework Boundaries

For React projects, React component and state discipline belongs in React skills.

For Next.js projects, do not apply Vite assumptions unless the project actually uses Vite tooling.

For TanStack Start projects, Vite config matters, but routing/server behavior belongs in TanStack Start skills.

## Review Checklist

When reviewing Vite config or project setup, ask:

- Is the config easy to understand?
- Is every plugin justified?
- Are aliases aligned with TypeScript?
- Are env vars safe for the browser?
- Are secrets kept out of `VITE_`?
- Is dev behavior hiding production behavior?
- Is this a tooling concern or app architecture concern?
- Can this config be simpler?
