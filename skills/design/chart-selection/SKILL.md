---
name: chart-selection
description: Choose effective charts and visual encodings for metrics, comparisons, trends, distributions, relationships, composition, and geographic data. Use when deciding how to visualize data, selecting chart types, or changing a chart's analytical meaning; not for cosmetic-only UI changes.
---

# Chart Selection

Own the analytical mapping from question and data to visual encoding. Do not own dashboard layout, implementation framework, or general UI polish.

## Establish the question

1. Identify the audience, decision, comparison, time horizon, and required precision.
2. Inspect actual field definitions, units, grain, aggregation, missingness, and sample size. Never invent metrics or data.
3. Distinguish observed values from forecasts, targets, percentages, rates, and cumulative measures.
4. If data is unavailable, give conditional recommendations and identify the minimal data needed.

## Choose by analytical task

Consult [chart decision matrix](references/chart-decision-matrix.md). Start with the task, not the chart library.

- Trend over time: line; bars for discrete periods or sparse observations.
- Compare categories: sorted horizontal bars or dot plot; table for exact values.
- Distribution: histogram, box plot, or density plot when justified.
- Relationship: scatter plot; add trend lines only when warranted.
- Part-to-whole: stacked bars for a few groups, 100% stacked for shares; avoid pies for precise comparison.
- Two-dimensional intensity: heatmap when both axes and color scale are meaningful.
- Geography: map only when location is analytically relevant, otherwise use ranked bars.
- Single value: KPI with units, time period, and relevant comparison; not a decorative gauge by default.

## Validate encoding

- Use a zero baseline for bar lengths; explain nonzero line baselines when consequential.
- Avoid dual axes unless independently scaled measures are indispensable and clearly labeled.
- Avoid 3D, misleading area encodings, unnecessary pie slices, rainbow palettes, and decorative complexity.
- Preserve consistent units, denominators, time zones, and category ordering.
- Show uncertainty, data gaps, and aggregation caveats where they affect interpretation.
- Use accessible labels and non-color cues; choose color scales that match quantitative, diverging, or categorical meaning.
- Do not claim causation from correlation.

## Output

For each proposed chart, provide: analytical question, fields and grain, chart type, encoding (x/y/color), aggregation, comparison/baseline, interaction only if useful, and trade-off. Prefer the simplest truthful option.

## Composition

- `dashboard-design` owns dashboard hierarchy and cross-chart interaction.
- `data-viz-review` independently checks interpretation and misleading presentation.
- `unslop` owns general visual consistency only when UI polish is relevant.
- Follow repository-local visualization and component conventions.
