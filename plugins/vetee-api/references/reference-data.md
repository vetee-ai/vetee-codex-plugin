# Reference data

Reference models supply IDs, codes and localized names for relationships,
targeting and labels. Resolve IDs from the selected environment; codes and
translated names are not interchangeable with IDs.

| Models | Meaning and important relations |
| --- | --- |
| `Locale`, `Country`, `Gender` | Language, country and gender dictionaries; localized names. |
| `Region` | Region linked to `country`. |
| `Currency` | Currency code used by prices/orders. |
| `AnimalSpecies`, `AnimalBreed` | Species and breed; breed links `animalSpecies`, not `species`. |
| `AnimalFoodType`, `AnimalInsuranceType`, `AnimalIntoleranceType`, `AnimalHypersensitivityType`, `AnimalEnvironmentType` | Profile classification dictionaries. |
| `AnimalEventType`, `AnimalFileType`, `AnimalIdentificationType`, `AnimalMeasurementType`, `AnimalMedicationType` | Event and attached record types. |
| `AnimalMedicationProduct` | Medication product reference. |
| `FacilityCategory`, `Specialization` | Facility grouping and veterinary specialization. |
| `ContentCategory`, `FileCategory` | Editorial and uploaded-file classification. |
| `LabelCategory`, `Label` | Label grouping and reusable labels. |
| `OfferTariff` | Entitlement tier used by offers and tariff-specific targeting/discounts. |

Inspect each model's live fields before assuming all have identical flags,
translations or create/update rights. Common list operations are
`getListLocale`, `getListCountry`, `getListAnimalSpecies`, etc.;
use explicit pagination and a stable order, usually `order` then `code`
where exposed. Retrieve `id code translations {id name locale {id code}}`.

Translations describe labels; they do not change a reference's semantic code.
Changing codes can affect filters and business logic. For a requested label
correction update the locale-specific translation instead.

AnimalBreed's code is unique within its species, not globally.
AnimalEventType also configures reminders, quick actions, expected attached
data and gender/species targeting; it is more than a display label.

- [Filters, translations and requested changes](reference-data/filters-and-translations.md)

