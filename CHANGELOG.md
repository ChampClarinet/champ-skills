# Changelog

## [Unreleased]

## [2.1.0] - 2026-11-27

### Added

- Add design skills for landing pages, visual refinement, chart selection, dashboard design, and data visualization review, with intent-based routing for UI work.
- Add `show-me` for choosing useful visual explanations, and `visual-verification` for checking rendered UI when appearance matters to acceptance.
- Add `verification` to ground acceptance criteria in authoritative requirements, select sufficient evidence, and distinguish verified outcomes from unverified claims.
- Add manual agent behavior evaluation cases and a protocol for recording baseline and candidate results.

### Improved

- Apply risk-based planning, bounded execution, meaningful checkpoints, and cut-loss and escalation guidance through `agent-orchestration` and `skill-router`.
- Track context and source authority across handoffs and resumptions, including a proportionate pre-execution assignment when material context would otherwise be lost.
- Allow proportionate maintainability work within the requested scope while preserving explicit ownership and decision boundaries.
- Capture reusable agent workflow lessons in post-mortems and route them to the appropriate tests, rules, skills, tooling, or evaluations.
- Support Codex skill discovery with `./scripts/link-skills.sh codex`, alongside Claude installation, and complete the published skill indexes.

### Fixed

- Preserve existing files and directories during skill installation; stop before linking if a target is not a symlink.
- Correct invalid `post-mortem` YAML frontmatter so the skill can be discovered by YAML-based tooling.
