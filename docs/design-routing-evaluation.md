# Design skill routing scenarios

These are behavioral acceptance scenarios for Codex skill discovery and composition. Run them with both design skills and skill-router installed.

| User request | Expected primary skill | Additional skill |
|---|---|---|
| Build a landing page for my SaaS waitlist | `landing-page-design` | framework skill only if needed |
| Design a new marketing hero with a clear signup CTA | `landing-page-design` | none by default |
| This existing dashboard looks AI-generated; polish it | `unslop` | relevant framework skill |
| Our current pricing page feels generic, preserve the copy | `unslop` | none by default |
| Fix the mobile overflow in this table | engineering / responsive implementation | `unslop` as scoped visual guardrail |
| Implement the provided Figma component faithfully | framework / Figma implementation | `unslop` as scoped visual guardrail |
| Build a new landing page, then audit the finished result | `landing-page-design` | `unslop` only for observed defects |
| Add a button to an existing settings screen | implementation skill | `unslop` as scoped visual guardrail |
| Refactor a backend database query | engineering skill | no design skill |

**Pass conditions:** one primary design owner, no forced double activation, explicit repository design tokens preserved, no invented proof, and at least one design skill activated for every UI task (including UI bug fixes), no unsolicited redesign, and no design skill required for non-UI work.

**Discovery check:** confirm `~/.agents/skills/landing-page-design/SKILL.md`, `~/.agents/skills/unslop/SKILL.md`, and `~/.agents/skills/skill-router/SKILL.md` resolve after running `./scripts/link-skills.sh codex`.
