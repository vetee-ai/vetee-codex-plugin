# Animals

`Animal` is the pet profile: `ownerUser`, `gender`, optional
`animalSpecies`, `animalBreed`, `avatarFile`, names and
`isOnboardingComplete`. The animal itself has no translations; its reference
models have localized labels. Birth and weight are related records, not direct
Animal scalar fields.

| Relations | Meaning |
| --- | --- |
| `animalUsers` | Per-user membership and role. |
| `animalFoods`, `animalInsurances`, `animalIntolerances`, `animalHypersensitivities`, `animalEnvironments` | Profile classification joins. |
| `animalEvents` | Dated history/plans, birth, reminders and recurrence. |
| `animalFiles`, `animalIdentifications`, `animalMeasurements`, `animalMedications` | Typed data attached to events and the animal. |

- [Membership and sharing data](animals/share-an-animal.md)
- [List and filter animals](animals/list-animals.md)
- [Inspect an animal](animals/get-an-animal.md)
- [Create an animal](animals/create-an-animal.md)
- [Update animal data](animals/update-an-animal.md)
- [Delete an animal](animals/delete-an-animal.md)
- [Animal events](animals/animal-events.md)

Admin visibility is broader than customer ownership. Always narrow by the
requested owner/animal, and return medical/user data only as needed.
See [shared conventions](reference-data/filters-and-translations.md).
