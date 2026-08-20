---
name: react-component-ownership
description: Apply ownership-boundary principles to React component architecture. Trigger proactively when creating or modifying React components with dialogs, tabs, forms, tables, query hooks, useState/useEffect, callbacks, shared fetching, nested composition, excessive component fragmentation, or Next.js client/server boundaries; especially when deciding whether state, effects, queries, mutations, handlers, UI zones, small render fragments, or `use client` belong in a parent or child component.
---

# React Component Ownership

Apply `ownership-boundaries` to React component architecture.

This skill is React-specific. Use it together with the framework-agnostic ownership skill when component ownership or decomposition is part of the task.

## Core rule

> Keep React state, effects, queries, mutations, and handlers in the narrowest component that actually owns the behavior.

Do not make a parent component the default controller for every nested workflow.

Also do not turn every small JSX fragment into a standalone component. Extract responsibility, not markup.

## Parent responsibility

Parents should primarily compose and coordinate children when coordination is genuinely their responsibility.

A parent may own shared state when multiple children must coordinate around the exact same value or transaction.

Do not hoist state, effects, or fetching merely because multiple components are rendered under the same parent.

For a large page or feature, the top-level component should usually describe the major zones and how they fit together rather than implement every nested detail itself.

## Hierarchical zone decomposition

Decompose large React surfaces recursively by meaningful UI and responsibility zones.

Typical shape:

```txt
Page
├─ Header
├─ SummarySection
├─ StockTab
│  ├─ StockTable
│  ├─ DetailsDialog
│  └─ EditDialog
└─ TransactionTab
   ├─ TransactionTable
   └─ DetailsDialog
```

The page should primarily compose `Header`, `SummarySection`, `StockTab`, and `TransactionTab`.

Then each zone may decompose again when its internal pieces have their own meaningful responsibility, lifecycle, state, reuse value, or rendering boundary.

Use this recursively:

```txt
page -> zones -> feature units -> smaller owned pieces
```

Do not flatten an entire screen into one component just because all JSX belongs to one route.

Do not over-split trivial markup that has no ownership, maintenance, reuse, or rendering benefit.

A good boundary makes it easier to answer:

- what this component is responsible for
- what state/effects belong here
- what children it coordinates
- what can change without understanding unrelated zones

## Meaningful component boundaries

A standalone component should normally have a reason to exist beyond making the parent file shorter.

Strong extraction reasons include:

- independent state, effects, lifecycle, queries, mutations, or event behavior
- a distinct workflow or feature responsibility
- meaningful independent reuse
- substantial rendering complexity that is easier to reason about in isolation
- a useful testing/review boundary tied to a real responsibility
- a justified rendering/performance boundary

Weak extraction reasons include:

- the JSX is a few lines long
- the fragment has a name
- the parent looks visually cleaner after extracting it
- every conditional branch is being turned into a component
- every option, label, table cell, badge, or value formatter is being moved to its own file

Tiny presentational fragments that are tightly coupled to one owner may stay inline or as a local render helper.

For example, an autocomplete option renderer that only chooses between a label and a two-line employee display usually belongs with the autocomplete owner rather than in a standalone `employee-option.tsx` component.

Use this test:

> If this fragment became a separate file, what independent responsibility would that file own?

If the answer is only "it renders these few lines of JSX," keep it local unless reuse, complexity, or measured rendering behavior provides another real reason.

## Performance-aware boundaries

Responsibility and ownership come first. Performance may justify an additional boundary when there is evidence or a predictable expensive subtree.

Useful performance reasons can include:

- isolating a subtree affected by frequently changing local state
- containing an expensive table, chart, editor, or other rendering-heavy unit
- making memoization practical at a meaningful boundary
- preventing unrelated zones from depending on rapidly changing state

Do not assume splitting a component or moving JSX into another file automatically improves React performance.

Do not introduce speculative `memo`, `useMemo`, `useCallback`, context, or component fragmentation without a real render/dependency reason. Prefer profiling or a clear render-frequency argument when performance is the motivation.

## Next.js client boundaries

In Next.js App Router code, default to Server Components and introduce `"use client"` only at the narrowest module boundary that actually requires client-only behavior.

A file normally needs `"use client"` when it directly uses client-only capabilities such as:

- `useState`, `useReducer`, `useEffect`, or other client-only React hooks
- browser APIs such as `window`, `document`, `localStorage`, or DOM event APIs
- interactive event handlers or client-side subscriptions that require a Client Component boundary
- client-only context/providers or libraries that require execution in the browser
- framework APIs that explicitly require a Client Component

Do not add `"use client"` merely because:

- the file exports a React component
- the component renders JSX
- the component receives props and displays data
- the component is imported by a Client Component
- another component in the same feature is a Client Component
- adding the directive feels safer

Being imported into the client module graph does not mean every descendant file should declare its own `"use client"` directive. The directive declares a client entry boundary; it is not a per-component annotation.

Prefer keeping the client boundary as low and narrow as practical. A server-renderable page, layout, section, or composition component should remain server-compatible when only a nested interactive unit requires the client runtime.

For example:

```txt
page.tsx                    # Server Component
├─ summary-section.tsx      # Server Component
└─ stock-filter.tsx         # Client Component: owns interactive filters
   └─ filter-label.tsx      # no `use client` unless this file directly needs it
```

Do not cascade `"use client"` across sibling or descendant files without a direct requirement.

When adding or preserving `"use client"`, be able to identify the concrete client-only dependency that justifies the boundary. If none exists, remove the directive unless an established framework/library constraint requires it.

When refactoring an overly broad client boundary, move client-only behavior into the narrowest meaningful interactive owner rather than converting the whole page or feature tree to client rendering.

Do not contort architecture solely to eliminate every Client Component. The goal is intentional, narrow boundaries, not zero client code.

## Local state and effects

Prefer keeping `useState`, `useReducer`, `useEffect`, subscriptions, timers, and lifecycle cleanup in the component whose UI or workflow requires them.

A useful test:

> If this child disappeared, would the parent still need this state or effect?

If no, the child or its dedicated hook is usually the better owner.

Avoid parents that accumulate:

- dialog open/close state for unrelated dialogs
- selected-row state used by only one child flow
- form state for nested forms
- effects whose only purpose is feeding a child
- loading/error state for queries the parent does not render
- handlers that simply call a child's workflow and are passed downward

## Queries and reusable hooks

Extract reusable data-access operations into hooks when multiple components need the capability.

Do not confuse a reusable hook with a shared query instance.

If `StockTab`, `BorrowDialog`, and `ReturnDialog` independently need stock data and do not require synchronized ownership, prefer each owner invoking the reusable stock query hook according to its own lifecycle rather than fetching once in the parent and drilling the result through props.

The same applies to other reusable queries such as employee, department, condition, lookup, or reference-data hooks.

Centralize query ownership only when shared synchronization, cache semantics, deduplication policy, transaction coordination, or rendering requirements actually demand it.

## Dialogs, tabs, forms, and feature units

Treat dialogs, tabs, forms, tables, sections, cards, and other workflow-oriented feature units as ownership candidates when they have meaningful independent behavior.

A dialog that owns a workflow should usually own its:

- open-local workflow state, unless an external trigger genuinely owns visibility
- form state
- validation
- query/mutation hooks
- loading/error handling
- selected entities used only by that dialog
- submit/cancel side effects

A tab with independent table behavior should usually own its:

- filters
- pagination/sorting
- table query state
- row-selection state
- details/edit dialog coordination specific to that tab

Do not split purely presentational fragments into components without a responsibility boundary just to reduce line count.

## Props and prop drilling

Props should express meaningful parent-child contracts.

Warning signs:

- a component receives a prop only to forward it unchanged
- several layers relay callbacks or query results without using them
- a parent owns data solely because a deep child needs it
- a child receives many unrelated state setters from the parent

Prefer moving ownership closer to the consumer or using an intentional shared boundary when coordination is real.

Do not introduce global context merely to avoid a small, meaningful prop contract.

## Avoid supercomponents

A React supercomponent is an ownership smell when it coordinates multiple unrelated workflows and accumulates their implementation details.

Before finishing a component-heavy change, inspect whether the top-level component has become responsible for:

- multiple unrelated forms or dialogs
- unrelated queries
- child-specific state/effects
- many child-specific event handlers
- large prop bundles whose fields belong to different workflows
- detailed implementation of multiple major page zones

If so, move each responsibility to its proper owner while preserving genuine shared coordination at the parent.

Avoid correcting a supercomponent by swinging to the opposite extreme and creating dozens of trivial leaf components with no independent responsibility.

## Relationship to file structure

Use `file-structure` together with this skill when creating or modifying project-owned React UI.

`file-structure` determines file boundaries and TypeScript/TSX naming/entrypoint conventions. This skill determines behavioral ownership, hierarchical decomposition, and intentional client/server boundaries.

One component per file does not mean every JSX fragment should become a component. First decide whether a meaningful component boundary exists; only then apply the one-component-per-file rule.

One component per file also does not by itself prevent a supercomponent if all state and effects remain centralized in the parent.

A folder `index.tsx` may be the composition entrypoint for a zone, but it should not become the dumping ground for every child implementation detail.

## Completion check

Before declaring React component architecture complete, confirm:

- major pages/features are decomposed into meaningful zones where appropriate
- each zone can decompose again according to responsibility rather than arbitrary line count
- tiny presentational fragments were not extracted solely because they contain JSX
- every standalone component has a meaningful responsibility, reuse, complexity, lifecycle, or justified rendering reason
- every added or preserved `"use client"` has a concrete client-only requirement
- client boundaries are as narrow as practical rather than copied through the component tree
- server-compatible parents/sections remain server-compatible when only a nested owner needs client behavior
- state is owned by the narrowest component that needs to coordinate it
- effects live with the workflow whose lifecycle triggers them
- reusable query logic is extracted without unnecessary centralization
- independently operating dialogs/tabs/forms can own their own hooks
- the parent primarily composes and coordinates rather than micromanaging children
- props represent meaningful contracts rather than relay chains
- performance-driven boundaries have an actual render/dependency reason rather than superstition
- no line-count rule was used as a substitute for responsibility analysis

## Interaction with other skills

- Always apply `ownership-boundaries` for the underlying architectural decision.
- Apply `scope-discipline` to avoid refactoring unrelated components.
- Apply `file-structure` for React and TypeScript/TSX file organization requirements.
- Apply `tooling-feedback` to actionable diagnostics in touched React code.
