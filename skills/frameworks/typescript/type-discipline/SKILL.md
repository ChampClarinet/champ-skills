---
name: typescript-type-discipline
description: TypeScript guidance focused on maintainable typing, explicit contracts, safe inference, modular type organization, and long-term readability.
---

# TypeScript Type Discipline

Use TypeScript to improve maintainability, correctness, tooling, and readability.

Do not use TypeScript to create clever unreadable type systems.

## Core Principles

- Prefer readability over type wizardry.
- Prefer explicit contracts.
- Prefer maintainable inference.
- Prefer predictable type ownership.
- Keep types close to their domain.
- Avoid unnecessary generic complexity.
- Optimize for future maintainers, not type gymnastics.

## TypeScript-First

Use TypeScript for project code.

Prefer typed APIs, typed component props, typed service boundaries, and typed domain models.

Avoid gradually falling back to untyped JavaScript patterns.

## Interfaces vs Types

Prefer interfaces for:

- component props
- object contracts
- domain models
- service/repository contracts
- extendable object shapes

Example:

```ts
export interface User {
  id: string;
  name: string;
}
```

Prefer type aliases for:

- unions
- mapped types
- utility compositions
- function signatures
- conditional types

Example:

```ts
export type Status = "idle" | "loading" | "success" | "error";
```

Do not argue dogmatically about `interface` vs `type`.

Choose the clearer representation.

## Avoid `any`

Avoid `any` whenever reasonably possible.

Prefer:

- `unknown`
- proper generic constraints
- explicit interfaces
- narrowing
- validation/parsing boundaries

If `any` is intentionally required, document why.

Bad:

```ts
const data: any = response.data;
```

Better:

```ts
const data: unknown = response.data;
```

## Type Narrowing

Prefer explicit narrowing before usage.

Example:

```ts
if (typeof value === "string") {
  return value.toUpperCase();
}
```

Do not blindly cast values just to silence TypeScript.

Avoid:

```ts
(value as User).name;
```

unless the boundary is trusted and intentional.

## Type Assertions

Use assertions sparingly.

Assertions should represent:

- trusted boundaries
- framework limitations
- validated external data

Do not use assertions to bypass real type problems.

## Utility Types

Use utility types when they improve clarity.

Good:

```ts
Partial<User>;
Pick<User, "id" | "name">;
Record<string, string>;
```

Avoid deeply nested unreadable utility compositions.

If a type becomes difficult to understand quickly, simplify it.

## Generics

Use generics intentionally.

Prefer simple readable generics.

Good:

```ts
function identity<T>(value: T): T {
  return value;
}
```

Avoid excessive generic abstraction layers that reduce readability.

Do not introduce generics unless they solve a repeated or reusable problem.

## Enums

Avoid enums for simple application states.

Prefer literal unions:

```ts
type Status = "idle" | "loading" | "success" | "error";
```

Use enums only when there is a clear interoperability or domain reason.

## File Organization

Keep small local types close to the implementation when tightly coupled.

Extract types when they are:

- shared across files
- domain-level concepts
- API contracts
- reused heavily
- large enough to distract from implementation logic

Examples:

```txt
user.types.ts
auth.types.ts
api.types.ts
```

Avoid giant global dumping-ground files like:

```txt
types.ts
global-types.ts
misc-types.ts
```

unless the scope is intentionally small and cohesive.

## Naming

Use descriptive type names.

Prefer:

```ts
UserProfile;
ApiError;
CreateUserPayload;
```

Avoid:

```ts
Data;
Item;
ResponseData;
Obj;
```

Boolean variables should use auxiliary verbs:

```ts
isLoading;
hasError;
canSubmit;
```

## Nullability

Handle `null` and `undefined` intentionally.

Prefer explicit optionality:

```ts
name?: string
```

Prefer narrowing before usage.

Avoid unsafe assumptions about existence.

## Async Typing

Prefer explicit async return types when clarity helps.

Example:

```ts
async function fetchUser(): Promise<User> {
  ...
}
```

Keep async data contracts typed across boundaries.

## Runtime Validation

TypeScript types do not validate runtime data.

For external data:

- APIs
- local storage
- query params
- user input

prefer validation/parsing when correctness matters.

Do not assume external data matches TypeScript types automatically.

## Inference Discipline

Allow TypeScript to infer obvious local values.

Good:

```ts
const count = 5;
```

Do not over-annotate trivial local variables.

Add explicit types when:

- the boundary matters
- readability improves
- inference becomes unclear
- exported APIs are involved

## Readability over Cleverness

Avoid:

- type puzzles
- unreadable conditional types
- deeply recursive types
- abstractions that only type experts understand

A simpler explicit type is usually better than a clever magical one.

## Review Checklist

When reviewing TypeScript code, ask:

- Is the type readable?
- Is this abstraction necessary?
- Would another developer understand this quickly?
- Is `any` avoidable here?
- Is inference helping or hiding intent?
- Is the type ownership clear?
- Is runtime validation needed?
- Is this type solving a real problem or creating one?
