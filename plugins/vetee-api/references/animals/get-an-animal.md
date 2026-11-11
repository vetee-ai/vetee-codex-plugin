# Inspect an animal

Use `getOneAnimal(filter: {id: $animalId})`; inspect `status` and `node`.
Read names, owner, species/breed/gender, avatar and memberships first.
Load only the related history/classification collections relevant to the task.

Birth is an `AnimalEvent` with an event type such as code `birth`.
Weight is an `AnimalMeasurement` with measurement type code `weight`;
its event supplies `occurredAt`. For latest weight, filter that type and
non-deleted records, order `animalEvent: {occurredAt: desc}`, limit one.
Consider null/estimated dates; newest creation time is not necessarily the
newest clinical observation.

Profile collections use their own type relations, e.g.
`animalFoods.animalFoodType`. Read translated names from those dictionaries.
`isOnboardingComplete` is stored state; the computed `isComplete` field
(where available) is separate.

Admin can see a profile that would not be available to a customer. Include
deleted state and membership checks in an access diagnosis.
See [Animals](../animals.md) and [Events](animal-events.md).
