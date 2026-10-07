# Skill Authoring v2

Write skills for capable agents: preserve non-obvious constraints and decision boundaries, remove explanations the model can reliably infer.

> Aggressively remove explanations. Conservatively remove constraints.

## Root skill contract

Every published `SKILL.md` must have YAML frontmatter with a concise `name` and `description`. The description should say what the skill governs and when it applies.

Keep `SKILL.md` at or below 500 lines. This is a champ-skills maintainability budget, not a platform limit. Treat approaching the limit as a signal to remove generic teaching or split conditional material.

A root skill should contain only what is useful on activation:

- purpose or core rule
- hard invariants
- decision rules the model cannot safely infer
- composition with canonical owners or adapters
- verification criteria
- explicit routes to conditional references when needed

Small skills do not need every heading.

## Hard constraints and guidance

Make the distinction obvious in prose.

A hard invariant is an intentional policy or safety/correctness boundary. Preserve it even when a different convention is common elsewhere, unless a higher-authority instruction overrides it.

Guidance expresses a preferred judgment and may yield to stronger local evidence.

Do not turn preferences into MUST language merely to make a skill sound authoritative.

## Progressive disclosure

Move examples, edge cases, templates, and specialized framework detail out of the root when they are not needed for every activation.

Prefer one shallow reference level:

```text
skill/
  SKILL.md
  references/
    edge-cases.md
  templates/
    report.md
```

The root must state when to read each reference. Avoid chains where one reference exists mainly to route to another.

## Composition

Do not copy a general engineering principle into every framework skill. Give the rule one canonical owner and let framework skills translate it only where framework mechanics matter.

Repository-local instructions override champ-skills. Cross-skill authority and conflict handling belong to `skill-router`, not bespoke precedence rules repeated in each skill.

## Ceremony

Every mandatory step must answer:

> What concrete failure mode does this prevent?

Keep mandatory sequencing when the prevented failure is material and the sequence meaningfully reduces that risk. Otherwise downgrade it to guidance or remove it.

Prefer executable guards such as tests, linters, CI, schema checks, or scripts over prose ceremony when they can enforce the same invariant more reliably.

## Verification loop

For deterministic work, prefer:

```text
perform → inspect against task + active invariants → fix → recheck
```

Skills should add only domain-specific acceptance criteria rather than duplicating a universal checklist.

## Evaluation

A refactor is successful only when it preserves intentional invariants while reducing unnecessary context or rigidity.

Test meaningful changes against realistic tasks. Compare correctness, constraint compliance, unnecessary changes, judgment quality, context cost, delegation quality, and resumability where relevant.
