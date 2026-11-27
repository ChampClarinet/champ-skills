# Chart decision matrix

| Analytical task | Default | Alternatives | Watch out for |
| --- | --- | --- | --- |
| Trend over continuous time | Line | Area for meaningful totals, bars for sparse periods | Unequal intervals, missing dates, truncated axes |
| Compare discrete categories | Sorted horizontal bar | Dot plot, table | Bar baseline must be zero |
| Rank entities | Sorted bar | Lollipop, table | Too many categories; unstable rankings |
| Distribution of one numeric variable | Histogram | Box plot, density | Bin width, sample size, outliers |
| Compare distributions | Box plot | Faceted histograms, violin with sufficient data | Hidden sample size and multimodality |
| Relationship between numeric variables | Scatter | Hexbin for dense points | Overplotting, correlation ≠ causation |
| Part-to-whole across groups | Stacked bar | 100% stacked bar for shares | Hard to compare middle segments |
| Part-to-whole at one moment | Bar showing shares | Donut only for a few coarse parts | Pie angles impede precise comparison |
| Two categorical dimensions and magnitude | Heatmap | Grouped bars for fewer categories | Unclear color scale or missing cells |
| Geography matters | Choropleth for normalized regional rates; proportional symbols for totals | Ranked bar if spatial pattern irrelevant | Raw counts on choropleths, area bias |
| Actual versus target | Bullet chart or paired bars | Dot plot | Unlabeled targets or mixed units |
| Exact lookup | Table | Table with in-cell bars | Chart not needed |
| Single headline metric | KPI with comparison and period | Sparkline alongside KPI | Missing context, ambiguous denominator |

## Decision checklist

1. What decision should a reader make?
2. Which measures and dimensions exist, at what grain?
3. Are values absolute, normalized, percentages, or cumulative?
4. Is exact lookup or pattern detection more important?
5. Which encoding makes the intended comparison easiest?
6. Could axis choices, aggregation, missing data, or color distort the conclusion?
7. Would a simpler table or chart communicate better?

## References

- Financial Times Visual Vocabulary: https://github.com/Financial-Times/chart-doctor/tree/main/visual-vocabulary
- Data to Viz: https://www.data-to-viz.com/
- W3C WCAG 2.2: https://www.w3.org/TR/WCAG22/

Use these as reference material, not as a substitute for inspecting the user's actual data.
