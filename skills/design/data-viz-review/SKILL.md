---
name: data-viz-review
description: Review charts and dashboards for misleading scales, incorrect aggregation, ambiguous metrics, poor comparisons, inaccessible encodings, and decision-making clarity. Use for data visualization audits and pre-ship reviews; do not redesign or change implementation unless requested.
---

# Data Visualization Review

Review-only by default. Evaluate whether a reasonable reader can draw a correct, useful conclusion from the visualized data.

## Inspect evidence

- Read the data schema, definitions, aggregation/query code, chart configuration, and rendered view when available.
- Separate verified defects from risks and unverified assumptions. Do not infer data correctness from a screenshot alone.
- Trace metric units, denominator, filters, null handling, time zone, sampling, and comparison windows back to source where possible.

## Audit

1. **Question fit:** Does the visual answer a specific question? Is a chart preferable to a table?
2. **Data fidelity:** Are aggregation, rates, missing periods, ordering, and outliers represented faithfully?
3. **Encoding:** Do bar baselines, axis ranges, scales, color mappings, and area/size encoding mislead?
4. **Comparability:** Are time windows, denominators, units, and categories comparable?
5. **Interpretation:** Are uncertainty, targets, projections, and causal limitations distinguishable?
6. **Accessibility:** Are labels, keyboard use, contrast, and non-color cues adequate?
7. **Dashboard behavior:** Do filters, refresh status, empty states, and drill-downs preserve context?

## Report

Order findings by severity and impact. For each finding provide location, evidence, why it matters, minimal fix, and verification method. Distinguish blockers from optional polish. State explicitly when a finding cannot be verified without underlying data or rendering.

Do not invent bugs or force changes merely to produce findings. If no material issues are found, say so and list coverage gaps.

## Composition

- `chart-selection` can propose replacements when a chart type is fundamentally wrong.
- `dashboard-design` owns major layout or information-architecture changes.
- `unslop` handles purely visual polish.
- `scope-discipline` applies if implementation changes are explicitly requested.
