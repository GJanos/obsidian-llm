---
description: Clean coding guidelines for all source files
paths:
  - "**/*.ts"
  - "**/*.tsx"
  - "**/*.sql"
  - "**/*.md"
---

## Comments

- Only add a comment when the WHY is non-obvious: a cost constraint, a subtle invariant, a workaround for a specific external behaviour, or a deliberate non-obvious omission.
- Never explain WHAT the code does — well-named identifiers do that.
- Never reference the current task, PR, or issue number in comments — those belong in commit messages and rot as the codebase evolves.

## Functions and scope

- One responsibility per function. If you need "and" to describe what it does, split it.
- Keep closures close to their use. Extract to a named function only when the logic is reused or the name adds meaningful clarity.
- Do not add parameters for values that are always the same at every call site.

## Dead code

- Delete unused code. Do not comment it out unless it is a deliberately reserved placeholder (document why in a comment).
- Do not keep variables, imports, or branches that are never reached.

## Scope creep

- Do not add features, refactors, or abstractions beyond what the current task requires.
- Three similar lines is better than a premature abstraction.
- Do not add error handling for scenarios that cannot happen given the current code's invariants.

## Configuration and defaults

- Parse and apply defaults once, at the entry point. Do not repeat `?? default` at every call site.
- Environment variable parsing belongs in `loadPulseConfig()`, not scattered across callers.

## Naming

- Names should state intent, not implementation. `fetchDigest` not `callApiAndParseJson`.
- Boolean variables and parameters should read as true/false assertions: `isArticleUrl`, not `articleUrlCheck`.
