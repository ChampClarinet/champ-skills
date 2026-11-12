---
name: dashboard-design
description: Design analytical and operational dashboards with clear decision goals, KPI hierarchy, chart composition, filters, drill-downs, responsive layouts, and useful empty/loading/error states. Use for new dashboards or substantial dashboard information-architecture changes; not for minor cosmetic fixes.
---

# Dashboard Design

Own dashboard information architecture, decision workflow, and cross-chart coherence. Delegate individual chart semantics to `chart-selection`.

## Define the job

1. Identify audience, recurring decisions, usage frequency, and primary questions.
2. Classify the dashboard: operational monitoring, analytical exploration, executive summary, or reporting. Mixed purposes need deliberate hierarchy.
3. Audit existing metrics, data definitions, filters, design system, and user permissions.
4. Ask only for missing information that would materially change the design; otherwise state assumptions.

## Structure

- Start with the decision and the most actionable exceptions; do not mechanically add KPI cards.
- Group related views into a clear reading order: overview, explanation, detail/action.
- Give every panel a question, title, metric definition, and meaningful time scope.
- Keep shared filters discoverable; distinguish global from panel-local filters and make applied state visible.
- Use consistent date ranges, units, denominators, and comparison periods across panels unless explicitly differentiated.
- Prefer a useful table or drill-down for precise investigation rather than packing every field into charts.
- Avoid redundant panels and dashboard sprawl.

## Interaction and states

- Choose filters, sorting, tooltips, drill-down, and cross-filtering only when they support a task.
- Design loading, empty, partial-data, stale-data, error, and permission-restricted states.
- Make refresh cadence and last-updated timestamps clear when freshness matters.
- Support keyboard navigation, readable labels, contrast, and responsive layouts; do not encode meaning by color alone.
- Preserve user context during navigation and filtering when feasible.

## Delivery

Produce a compact dashboard specification before implementing when the task is non-trivial:

- Audience and top decisions
- KPI definitions and data sources (or explicit unknowns)
- Panel inventory: question, chart/table, dimensions, metrics, aggregation
- Global and local filters, interactions, states
- Layout hierarchy, responsive behavior, accessibility notes
- Validation plan with representative data, edge cases, and actual rendering

Implement within existing project conventions; no speculative dependencies or broad redesign.

## Composition

- Use `chart-selection` when choosing or changing chart semantics.
- Use `data-viz-review` when asked to audit the dashboard's truthfulness or analytical clarity.
- Use `unslop` for visual consistency, especially when modifying an existing dashboard; it does not replace analytical design.
- Use `scope-discipline` for repository modifications.
