# Admin filters, translations and changes

Use [GraphQL workflow](../graphql.md) for environment selection, introspection
and the read-only default. Confirm these API patterns against the selected
environment's authenticated schema.

## Admin visibility and filters

Set the requested user/record scope, active/deleted state and date conditions
explicitly. Do not use an administrative result as proof of customer visibility.
Select only data relevant to the task.

- Scalar list filters use objects: `id: {equals: $id}`, `isActive: {equals: true}`,
  text `contains` with `mode: insensitive`, numeric/date `gte`, `lt`, etc.
- A nullable scalar can be filtered with `null`, e.g. `deletedAt: null`.
- Singular relations nest the referenced model: `user: {id: {equals: $id}}`.
- List relations use `some` (at least one), `none` (no match), or `every`
  (all match, also true for an empty collection).
- Combine independent criteria in `AND`; alternatives in `OR`. A `some`
  condition does not match an empty collection.
- `getOne<Model>` uses a unique filter such as `{id: $id}`, without `equals`.
  Do not assume a non-unique code is a unique key.
- Filter parents with `translations: {some: {...}}`. A filter on selected
  `translations(...)` narrows returned translations, not parent records.

For publication windows, the customer-facing convention is
`publicFrom <= now < publicTill`; null boundaries are unrestricted. Build each
boundary as an `OR` between null and a date comparison. Add active/deleted
conditions separately, including on join records when relevant.

## Translations and targeting

Translations hold localized text/media. Each links its parent through
`object` and language through `locale`; usually one row per parent/locale
is enforced. Return translation IDs and `locale {id code}` before an edit.

`localeFilters` are audience join records, not translations. Likewise
`countryFilters`, `genderFilters`, `animalSpeciesFilters`, `partnerFilters`
and `offerTariffFilters` select audiences where present. Each join usually
has `object`, a reference and `isActive`. Adding translated text does not
create or enable a targeting row.

Select a language with
`translations(filter: {locale: {code: {equals: "cs"}}})`. A missing translation
returns an empty collection; fallback is a caller decision. `nameUnaccent`,
where exposed, is an accent-free search companion to `name`: normalize the
search term too. Case-insensitive mode alone does not remove accents.

## Requested changes

Only execute writes explicitly requested by the user. Introspect concrete
inputs: readable fields are not necessarily writable.

Current generic updates take scalar values directly, e.g.
`data: {isActive: false}`. Singular relations
typically use `{connect: {id: $id}}`; disconnect and collection shapes depend
on the relation. For fields whose state must be preserved, follow the domain's
update instructions and verify the resulting values.

Update a translation by its own ID through `updateOne<Model>Translation`
when available; create a missing one with `createOne<Model>Translation`,
`object: {connect: {id: $parentId}}` and
`locale: {connect: {id: $localeId}}`. Resolve existing joins before creating:
parent/reference pairs often have unique constraints. Do not replace all
translations or targeting rows to change one entry.

Generic `deleteOne<Model>` performs soft deletion, reflected in `deletedAt`.
Do not interpret it as permanent erasure of all related data.
Verify parent and related records separately. Prefer deactivation when
that is what the user requested.

Check GraphQL errors and `status`, then read back changed fields.
For a requested business action, use its documented dedicated operation rather
than simulating it through generic record edits.
