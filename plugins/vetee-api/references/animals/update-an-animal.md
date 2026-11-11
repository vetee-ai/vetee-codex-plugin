# Update animal data

For a requested edit, resolve the Animal ID and current values first.
Introspect `Input_UpdateData_Animal`, then call `updateOneAnimal` with the
unique `filter` and only requested `data`.

Scalar edits use direct values, e.g. `data: {callName: $name}`. Reference
changes use the available relation input, typically
`animalBreed: {connect: {id: $breedId}}`. Verify that the selected breed
belongs to the intended species; changing species does not inherently choose
a compatible breed.

Profile type joins are independent records. Edit the correct AnimalFood,
AnimalInsurance, AnimalIntolerance, AnimalHypersensitivity or AnimalEnvironment
row instead of replacing all profile collections. Translations belong to
reference models, not Animal.

Owner changes must account for `animalUsers` roles. History corrections target
the event and attached record, not the profile. Read back changed values and
related IDs after success.
See [Animals](../animals.md) and [shared inputs](../reference-data/filters-and-translations.md).
