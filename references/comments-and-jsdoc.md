# Comments and JSDoc

## Implementation comments

- Preserve the author's wording and intent, including comments that moved with code. Revise the smallest stale detail. Explain why a surprising decision exists, what invariant is protected, and which concrete case would fail without it. Say where a value actually comes from after tracing its owner.
- Prefer same-line comments when the project uses them. Put the rationale for a block on its introducing line. On multiline strings, place the comment outside the closing delimiter. Keep strictly parsed JSON valid and record rationale at the owner, importer, or adjacent docs. Check that formatting preserves the comment's location and meaning.
- Use the project's purpose labels. A useful convention is `Bug:` for verified previous behavior, `Fix:` for how the current code corrects it, `Note:` for current behavior, `Decision:` for a trade-off, and `Rejected:` for a design that should stay out. Lead with the quick point, then give the reason or example. Describe hypothetical risks as such. Follow local rules on decision references and keep private provenance out of public artifacts.
- Use the owner's terminology and explain verified user terms beside their implementation when useful for search. When reusing an established pattern, name the actual counterpart. For an explicitly rejected behavior or design, record the rejection and reason at the simplified boundary so it is not gradually reintroduced.
- Mark moved or extracted code clearly at the declaration, and on new files where the project uses a move history header. Name the old path or symbol. Mark what changed behavior separately. Keep pure moves reviewable on their own where the workflow supports it. Verify that former comments remain attached to the corresponding implementation.

## Caller-facing documentation

- Put JSDoc immediately above a named declaration or its decorators. Start with the caller's result or effect, using names and language consistent with the code. Give named functions and class methods a short summary. Apply the same standard when materially changing an existing callable, including a private helper whose contract is hard to infer.
- Mention prerequisites, lifecycle, absence, ordering, side effects, unusual units/parameters, and failures when a caller needs them. Describe what a predicate proves or what a callback should return. Avoid duplicating a clear signature. Prefer a short `@example` only where a concrete call sequence or unusual input helps.
- Use `@param`, `@returns`, and `@throws` for additional caller information. Avoid repeating the TypeScript type, listing implementation steps, or promising errors the implementation cannot throw. Check early exits and alternate branches before making a guarantee.

```ts
/** Returns the last saved search, or undefined before the first save. */
function getLastSavedSearch(savedSearches: readonly string[]): string | undefined {
  return savedSearches.at(-1);
}
```

Read the final diff for orphaned comments, confusing historical tense, stale source claims, missing decision rationale, and JSDoc attached to the wrong symbol. Include specs, scripts, and template comments when relevant.
