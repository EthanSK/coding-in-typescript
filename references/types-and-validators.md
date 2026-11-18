# Types and validators

## Derive from the owning contract

- Search for the existing model, DTO, schema, form value, or function result before adding or changing a type, including a generic argument. Use indexed access, `Pick`, a checked `Omit`, `Required`, `Partial`, `NonNullable`, or `ReturnType` only for the transformation needed. Preserve field layout as well as value types. A different external format belongs in an explicit adapter.
- Standard `Omit<T, K>` accepts unknown keys. Check the exclusion with `keyof Pick<T, K>` or the repository's equivalent. A conditional such as `Extract<T, { misspelled: unknown }>` may quietly become `never`, and `keyof never` is broad. A broad string index signature also accepts arbitrary names. Select from the declared owner or meaningful union member.
- Compose a shared capability when the fields have the same meaning across actual owners. Check every applicable model, reader, and writer, including required and optional variants. Shared spelling alone does not establish shared semantics. Keep an independently inferred internal shape when it is the source of truth for that shape.
- Check fresh literals where constructed, including optional and nested fields, callback returns, partial writes, computed keys, and conditional fragments. An annotated enclosing object may still accept a misspelled key introduced through a spread.

```ts
type SearchOptions = {
  query: string;
  limit?: number;
  sort?: 'recent' | 'title';
};

type PublicSearchOptions = Omit<SearchOptions, keyof Pick<SearchOptions, 'limit'>>;

declare const useRecentSort: boolean;
const sortOptions = useRecentSort
  ? ({ sort: 'recent' } satisfies Pick<SearchOptions, 'sort'>)
  : {};
const searchOptions: SearchOptions = { query: 'guide', ...sortOptions };
```

## Check known runtime keys

- Prefer direct typed access or an existing semantic guard when it expresses the same check. For changed known-key strings in `in`, own-property checks, bracket access, reflection, queries, fixtures, and test matchers, check against the owning contract. For a literal already intended to name exactly one key, select that key explicitly so replacing just the expression with a different valid key still fails. Use an existing checked union-key helper or the intended union member when a key exists on only some variants.
- For nested field paths, check every segment, including the parent. Check query values against the indexed field type as well as checking the key. At SDK boundaries, derive overridden field names from the real SDK type too. Add a locally declared SDK gap only after confirming the specific endpoint's documented schema.
- Preserve runtime semantics. Existence, own-property, definedness, and truthiness answer different questions. Dynamic dictionaries, unknown external schemas, and tests deliberately asserting that a removed key is absent have different contracts. Explain a genuine unchecked exception where it occurs.

```ts
declare const candidate: object;
const hasSort = ('sort' satisfies keyof Pick<SearchOptions, 'sort'>) in candidate;

type Account = { preferences: { emailUpdates: boolean } };
const emailUpdatesField =
  'preferences.emailUpdates' satisfies
    `${keyof Pick<Account, 'preferences'>}.${keyof Pick<Account['preferences'], 'emailUpdates'>}`;
```

## Make valid states explicit

- Use the existing literal, enum, or boolean as discriminator when one property determines the valid payload. Separate unfinished records from completed records when writers guarantee different fields. Trace creation, transition, reset, and error paths before strengthening or relaxing requiredness. A recorded request proves admission only. A false flag can coexist with the date of a past event when the product retains history.
- Derive branch payloads from owning fields. Reuse checked capability helpers for genuine repetition. Preserve the discriminator through creators, return values, projections, partial updates, and spreads. Use a distributive derivation when ordinary `Pick` or `Omit` would flatten the union. Avoid enumerating combinations of independent settings.
- For a closed union, handle every case explicitly. Prefer the established exhaustive lint/compiler check or a `never` assignment after the switch. Omitting a catch-all branch alone does not enforce coverage. Use a genuine fallback only for a documented open-ended input or expected missing case. Give semantic predicates a narrowing return type only when their runtime test actually proves it.
- Keep IDs distinct from optional snapshots of the entities they identify. Preserve intentional distinctions between null, undefined, omission, and a field forbidden in a particular branch. Check what serialization and the target compiler options actually preserve.

## Type and validate at the boundary

- Follow the project's runtime schema or validation architecture. Derive types from the authoritative schema when supported, or check the validation configuration against the owning type where the type is authoritative. Treat external payloads, persisted data, and untyped SDK results as `unknown` until validated. Preserve generic information in the helper where it was lost instead of casting each consumer. A type assertion is never runtime validation.
- Keep request DTOs data-only when compatible with the framework. Assemble checked payloads directly, preserve meaningful constructors, and remove copying constructors only in scope. A framework initialization assertion or decorator alone does not prove a payload is valid.
- Keep one shared finite-choice contract for stored values, forms, DTOs, and validator lists. A list checked with `satisfies readonly SomeField[]` checks membership. If all variants must be accepted, derive the union from the canonical list or verify exhaustiveness separately. Keep aggregates and arbitrary numeric measures distinct from finite domain values.

## Prove the checks work

Compile the valid baseline in the owning configuration, including changed specs. In isolated copies or temporary probes, misspell the literal and its selected key independently, substitute another valid key at an exact-key check, rename each nested segment, and try an incompatible value. Cover every changed conditional spread fragment and each changed owning-key form. For unions, try missing required fields, forbidden combinations, and a new unhandled variant. Require diagnostics at the intended site. Remove the probes before handoff.

### Exhaustiveness example

```ts
type UploadState =
  | { kind: 'queued' }
  | { kind: 'complete'; fileSize: number }
  | { kind: 'failed'; reason: string };

function describeUpload(upload: UploadState): string {
  switch (upload.kind) {
    case 'queued':
      return 'Queued';
    case 'complete':
      return `Stored ${upload.fileSize} bytes`;
    case 'failed':
      return upload.reason;
  }
  const unhandledUpload: never = upload;
  return unhandledUpload;
}
```
