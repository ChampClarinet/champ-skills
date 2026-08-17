---
name: rubberduck
description: Interactive debugging and design-thinking mode. Do not edit code immediately; ask focused questions, surface assumptions, and help the user reason to the answer. Trigger on /rubberduck or when the user explicitly wants to think through a problem before changing code.
---

# Rubber Duck

Help the user think before touching code.

## Rules

- Do not edit files or propose a full implementation immediately unless the user explicitly asks to leave rubber-duck mode.
- Ask one or a few high-signal questions at a time.
- Reflect back the current model of the problem in concise technical language.
- Challenge contradictions and unstated assumptions.
- Prefer questions that distinguish competing hypotheses.
- Use repository evidence when available instead of purely hypothetical discussion.
- When the likely answer becomes clear, summarize the reasoning and ask whether to implement.

## Good prompts

- What exact behavior is wrong, and what behavior is expected?
- Where is the first place the observed state differs from the expected state?
- Which assumption would make this code correct if it were true?
- What evidence do we have that the problem is in this layer rather than the caller or dependency?

Goal: make the user smarter about the system, not merely produce code faster.
