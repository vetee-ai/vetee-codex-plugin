# List and filter facilities

Use `getListFacility` with `Input_Filter_Facility`, order and pagination.
Useful criteria include category, country, region, owner, active/deleted state,
emergency flags and translated name/address.

```graphql
query InspectFacilities($filter: Input_Filter_Facility, $pagination: Input_Pagination) {
  getListFacility(filter: $filter, order: {order: asc}, pagination: $pagination) {
    status { success errorCode errorMessage }
    meta { limit offset total }
    nodes {
      id name city isActive deletedAt gpsLatitude gpsLongitude
      facilityCategory { id code }
      country { id code }
      translations { id name city locale { id code } }
    }
  }
}
```

Filter examples:

- `facilityCategory: {code: {equals: $code}}`.
- `ownerUser: {id: {equals: $userId}}`.
- `translations: {some: {nameUnaccent: {contains: $normalizedTerm, mode: insensitive}}}`.
- `specializationFilters: {some: {isActive: {equals: true}, specialization: {id: {equals: $id}}}}`.

Other targeting uses `localeFilters` and `animalSpeciesFilters`.
Searching a selected translation does not filter parent facilities unless
the condition appears in the parent filter.
See [Facilities](../facilities.md) and
[shared conventions](../reference-data/filters-and-translations.md).
