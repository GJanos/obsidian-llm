---
description: TypeScript coding guidelines for all .ts and .tsx files
paths:
  - "**/*.ts"
  - "**/*.tsx"
---

## Types

- No `any`. Use `unknown` for truly unknown input; use a narrow structural type (e.g. `{ warn(msg: string): void }`) for constrained duck-typed values.
- Use `import type` for type-only imports so they are erased at compile time.
- Keep interface fields non-optional unless absence is a genuinely valid runtime state. If a field always has a value after initialization, make it required.
- Prefer structural types inline over named type aliases for narrow, single-use constraints.

## Async

- Use `Promise.allSettled` when partial failure is acceptable and the successful results should still be used.
- Use `Promise.all` only when all-or-nothing semantics are correct.
- Never swallow rejected promises silently — log or rethrow.

## Inference

- Let TypeScript infer return types and array element types where the inference is unambiguous (e.g. `flatMap` narrowing).
- Only annotate explicitly when the inferred type would be `never[]`, `any`, or misleading.

## Imports

- Group: external packages → internal modules → types. One blank line between groups.
- No barrel re-exports unless the module surface genuinely warrants it.

## Error handling

- Throw `Error` with a descriptive message at system boundaries (API responses, config parsing, missing env vars).
- Do not add try/catch around code that cannot throw under normal conditions.
- `errBody` pattern for HTTP errors: `await res.text().catch(() => '(unreadable)')` — always safe to include in thrown Error message.
