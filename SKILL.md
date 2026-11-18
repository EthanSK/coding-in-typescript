---
name: coding-in-typescript
description: Write, change, or review TypeScript code in any repository. Use for work on types, model and API contracts, runtime validators, services, frontend code, tests, refactors, comments, and JSDoc. Follow the target project's instructions, tooling, and established patterns.
---

# Coding in TypeScript

Make the smallest complete change that preserves the owning contracts and lets the compiler catch mistakes at the point they are made. Use this skill during implementation and review. For ordinary questions about existing code, answer from the source.

## Continuous improvement

When the user explicitly states a general preference for this skill, preserve their wording, rationale, and scope in the appropriate guidance. Treat verified findings as candidates when they prevent a serious mistake or will save meaningful repeated work. Refine the relevant rule in the same task when authorized, and avoid accumulating incident history or duplicate rules. Retest the affected guidance, validate the package, and keep conditional detail in directly linked references. Mark material agent-originated changes with their date, reason, and shareable evidence. Keep private evidence in the user's private records.

## Skill usage announcement

Before using the skill, tell the user its name and why it applies unless they asked for silent use. Follow their established announcement format when available.

## Weekly public updates

On first use in a task, or at the next use after a week, follow the [public update procedure](references/public-updates.md). Respect opt-outs and permissions, preserve local edits, and avoid force, reset, discard, or plugin-cache writes. Ask before installing an available update and tell the user what changed after installation. A check authorizes no update or project action.

## Workflow

1. Read the local instructions, the owning code and contracts, the normal entry points, and at least one nearby example where available. Trace the producers, consumers, and tests affected by the task. Use the repository's package manager, task runner, compiler configuration, and formatter. Separate proven existing patterns from code introduced in the current diff.
2. Keep changes surgical. Reuse or extend the actual owner. Keep generic modules generic and feature behavior at its owning feature or call site. Choose routine implementation details yourself. Get a decision before making a consequential change to architecture, data meaning, privacy, or another surface. For a cycle between libraries, show the exact import chain and placement options before changing the affected architecture.
3. Keep one source of truth for property names, types, requiredness, and layout. Reuse the complete contract when it fits. Derive only the fields the caller needs. Use checked selections for keys, including excluded keys, runtime key strings, nested path segments, and fresh object fragments before spreading. A renamed or misspelled key should fail where it was used. Keep a new one-use parameter shape inline when it helps readability.
4. Model real variants with discriminated unions. Keep tags paired with their payloads through creation and projection. Handle closed switches exhaustively, with compiler enforcement and explicit cases. Preserve the meaning of missing, null, unfinished, failed, and completed values. Narrow or validate untyped data at its boundary. Use assertions only for a concrete boundary or compiler limitation that remains after preserving the available types. Never silence a mismatch with double casts, invented defaults, or a widened production contract.
5. Name things for what they are. Put the file's foundational declarations and core operations before supporting details. Keep service-owned helpers and constants inside the service when that is the local class pattern. Preserve existing comments. Explain non-obvious choices beside the owning code, using same-line comments where the repository supports them. Give new and materially changed named functions and methods concise, caller-focused JSDoc under the project conventions.
6. Check the entire in-scope diff, including tests and earlier edits. Confirm ownership, the canonical types, and the normal entry points. Remove speculative helpers, redundant reads and guards, and unneeded compatibility code. Any retry, fallback, rollback, or extra guard needs a concrete reachable failure and an explanation beside the code. Never weaken production code to make a test easier. Run the relevant checks and report which scope passed, along with any gap.

## Read for the work at hand

- [Types and validators](references/types-and-validators.md) for model derivations, finite choices, unions, known keys, SDK boundaries, or negative compile checks.
- [Ownership and structure](references/ownership-and-structure.md) for module placement, imports, shared behavior, scripts, naming, or moving code.
- [Data, APIs, and operations](references/data-apis-and-operations.md) for storage, migrations, queries, pagination, authorization, errors, retries, or concurrency.
- [Comments and JSDoc](references/comments-and-jsdoc.md) for explanatory comments, documentation, bug fixes, or refactor provenance.
- [Frontend](references/frontend.md) for UI state, forms, controls, browser storage, styling, or Angular work.
- [Tests and review](references/tests-and-review.md) for specs, verification, behavior-changing work, or code review.
- [User preferences](user-preferences.md) when a material choice depends on private preference history and the user has an established store.
