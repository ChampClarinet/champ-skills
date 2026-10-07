---
name: typescript-type-discipline
description: Champ's TypeScript defaults for readable contracts, any/unknown, assertions, runtime validation, inference, enums, and type ownership. Use when type design or TypeScript boundaries require a policy decision.
---

# TypeScript Type Discipline

Use types to make contracts and ownership clearer, not to demonstrate type-system cleverness.

Repository-local explicit conventions override these defaults.

## Readability first

Prefer the simplest type that accurately communicates the contract.

Avoid type puzzles, deeply recursive machinery, and generic abstraction whose maintenance cost exceeds the correctness or reuse it provides.

Do not add generics merely because code can be generalized. Generalize when callers share the same concept and the abstraction remains readable.

## Interface and type defaults

Under Champ defaults, prefer interfaces for ordinary object contracts, component props, domain models, and service/repository contracts.

Prefer type aliases when unions, mapped/conditional types, utility composition, intersections, or function signatures make them clearer.

This is a readability default, not a reason to churn an established repository convention.

## `any`, `unknown`, and assertions

Avoid `any` whenever reasonably possible.

At uncertain boundaries, prefer `unknown` plus narrowing or validation.

Use assertions only when the value is already justified by a trusted/validated boundary or a framework limitation. Do not cast merely to silence a type error.

If `any` is genuinely required at a boundary, keep it narrow and make the reason evident from nearby code or repository convention.

## Runtime boundaries

TypeScript types do not validate runtime data.

Validate or parse untrusted/external data when correctness depends on its shape, including API responses, storage, query parameters, user-controlled input, and other runtime boundaries.

Do not add runtime schemas to internal values whose shape is already guaranteed merely for ceremony.

## Inference and explicit contracts

Use inference for obvious local implementation details.

Prefer explicit types where a public/exported boundary, service contract, domain boundary, async result, or otherwise non-obvious shape benefits from clarity.

Do not annotate trivial locals simply to make them look typed.

## Type ownership

Keep small types close to the code that owns them.

Extract a type when it is an independently meaningful domain/API contract, shared by multiple owners, or large enough that colocation obscures the implementation.

Do not create broad `types.ts`, `common.ts`, or similar dumping grounds for unrelated contracts.

`file-structure` remains the canonical owner of file organization and naming.

## Enums

Prefer literal unions for simple application states.

Use enums when interoperability, generated/external contracts, or a domain requirement gives the enum itself concrete value.

Do not migrate existing enums solely to satisfy this preference.

## Nullability

Model optional or nullable values intentionally.

Narrow before use rather than hiding uncertainty behind non-null assertions.

Use a non-null assertion only when an invariant genuinely guarantees the value and that invariant is clear at the usage boundary.

## Composition

- `ownership-boundaries` owns who owns a contract.
- `file-structure` owns where independently owned types live.
- framework skills own framework-specific typing constraints.
- `tooling-feedback` owns TypeScript/compiler diagnostics on touched code.

This skill should not repeat basic TypeScript syntax or utility-type documentation.

## Verification

For touched type design, verify:

- the contract is readable without type gymnastics
- `any` and assertions are narrow and justified
- runtime data is validated where static typing cannot guarantee it
- inference is used for implementation detail, explicit types for meaningful boundaries
- extracted types have independent/shared ownership
- nullability is handled explicitly
- repository convention was not churned for a personal syntax preference
