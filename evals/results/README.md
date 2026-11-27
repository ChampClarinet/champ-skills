# Evaluation results

Track meaningful baseline/candidate comparisons and model or skill regressions, not every development session.

Store one Markdown report per evaluation campaign, named YYYY-MM-DD-<short-label>.md. Do not create a dated report until an evaluation actually runs.

## Report template

- Date and evaluator:
- Baseline and candidate skill revisions (commit or tag):
- Model/version and effort for each:
- Environment, fixture revision, available tools, discovery/install method:
- Case/rubric revision:
- Run counts and deviations:

| Case / run | Baseline | Candidate | Evidence reference | Notes |
|---|---|---|---|---|
| Case ID / run ID | Pass / Fail / Unverified | Pass / Fail / Unverified | Sanitized trace or artifact reference | Material differences |

Summarize improvements, regressions, unchanged behavior, and unverified coverage separately. Include actual pass/fail/unverified counts and denominators; do not treat unverified as passed or omit failed runs. Preserve individual run outcomes when repeated runs disagree.

Record the decision and any proposed follow-up. Keep reports comparable; explain differences in model, fixture, rubric, tools, or conditions that limit attribution. Do not overwrite historical results to reflect later policy changes. Correct errors transparently.

Keep only concise, sanitized evidence references in Git. Do not commit raw session transcripts, secrets, private project data, or large runtime artifacts by default. If evidence cannot be shared, state the limitation.
