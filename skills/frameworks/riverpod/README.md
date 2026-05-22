# Riverpod skills

Riverpod-specific state management, provider structure, and dependency flow guidance.

Riverpod skills should keep state management explicit, maintainable, testable, and easy to reason about.

## Philosophy

- Use providers intentionally
- Prefer local widget state when state is truly local
- Avoid unnecessary provider proliferation
- Keep provider ownership clear
- Keep async state predictable
- Make dependencies explicit and testable
- Avoid Riverpod ceremony when simpler Flutter state is enough

## Skills

- **[provider-discipline](./provider-discipline/SKILL.md)** — Riverpod state management guidance focused on intentional provider usage, state ownership, async state, dependency flow, performance, and testability.
