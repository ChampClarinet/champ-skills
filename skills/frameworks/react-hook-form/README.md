# React Hook Form skills

React Hook Form guidance for form state ownership, validation, controlled/uncontrolled inputs, schema validation, and maintainable form workflows.

React Hook Form skills should keep forms predictable, performant, explicit, and easy to maintain.

## Philosophy

- Prefer React Hook Form for non-trivial forms
- Keep form ownership explicit
- Prefer uncontrolled inputs when practical
- Keep validation centralized and predictable
- Avoid unnecessary form re-renders
- Prefer schema-driven validation for complex forms
- Keep form state local to the form/module when possible
- Avoid turning forms into giant effect-driven workflows

## Current Stack

Current preferred stack commonly includes:

- React Hook Form
- TypeScript
- shadcn/ui

These are preferences, not hard requirements.

## Skills

- **[form-discipline](./form-discipline/SKILL.md)** — React Hook Form guidance focused on form ownership, validation, schema usage, field organization, async submission, and maintainable form workflows.
