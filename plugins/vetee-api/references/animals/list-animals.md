# List and filter animals

Use `getListAnimal` with `Input_Filter_Animal`, order and pagination.

```graphql
query InspectAnimals($filter: Input_Filter_Animal, $pagination: Input_Pagination) {
  getListAnimal(filter: $filter, order: {createdAt: desc}, pagination: $pagination) {
    status { success errorCode errorMessage }
    meta { limit offset total }
    nodes {
      id callName givenName kennelName deletedAt
      ownerUser { id }
      animalSpecies { id code translations { name locale { code } } }
      animalBreed { id code }
      gender { id code }
    }
  }
}
```

Useful filter fragments (supply IDs through variables):

- Owned: `ownerUser: {id: {equals: $userId}}`.
- Membership: `animalUsers: {some: {deletedAt: null, user: {id: {equals: $userId}}}}`.
- Species: `animalSpecies: {code: {equals: "dog"}}`.
- Name: `callName: {contains: $term, mode: insensitive}`.
- Live animals: `deletedAt: null`.

Owner and membership are different predicates; use `OR` only if the task
requires either. Admin queries are not automatically limited to the caller.
Page to `meta.total` when a complete count/list is requested.
See [Animals](../animals.md) and [filters](../reference-data/filters-and-translations.md).
