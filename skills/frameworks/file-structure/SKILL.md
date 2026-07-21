---
name: file-structure
description: Mandatory file organization rules for maintainable component and class structure.
---

# File Structure

Use one primary class or component per file.

## Non-Negotiable Rules

- One Flutter widget class per file.
- Exactly one project-owned React component per file.
- One domain, service, or model class per file.
- File names must match the primary class or component name.
- Never group multiple project-owned React components in one file, even when they are small, private, closely related, used only once, or compose a single screen.
- Extract every additional project-owned React component into its own file and import it.
- Do not treat