# Agent behavior evaluations

These are repository-level behavioral regression cases, not installed skills or application tests.

## Run protocol

Use a fresh isolated session and disposable fixture for each case. Install the candidate skills through the normal discovery mechanism. Do not expose the expected rubric to the evaluated agent. Give it only the task and fixture conditions. Record model/version, effort, skill revision, environment, available tools, actual tool calls/results, final response, and deviations. Do not expose secrets or use production systems.

Compare baseline and candidate under equivalent conditions. Repeat when nondeterminism matters. Score each required behavior pass, fail, or unverified from observable evidence; a missing trace is not a pass. A case passes only when all required behaviors pass. Report individual outcomes and run counts, not unsupported aggregate claims.

The initial cases are manual evaluation specifications. No automated agent runner or fixture implementation is supplied yet. Prepare the stated fixture before running a case; if unavailable, mark it unverified. Do not claim runtime coverage from reviewing this document.

Add cases for consequential recurring failures or meaningful policy changes. Prefer a minimal reproducible scenario and observable rubric over a transcript. Keep application regressions in application tests. Never weaken a rubric merely to make a candidate pass.
