# Attach data to an animal event

Each attachment links **both** `animal` and required `animalEvent`.
Confirm the event belongs to that animal before any requested insert/update.

| Model | Type relation and payload |
| --- | --- |
| `AnimalFile` | `animalFileType`, `file`, optional description. |
| `AnimalIdentification` | `animalIdentificationType`, string `value`, description. |
| `AnimalMeasurement` | `animalMeasurementType`, numeric `value`, `isEstimatedValue`, description. |
| `AnimalMedication` | `animalMedicationType`, optional `animalMedicationProduct` and model-specific fields. |

Use `getList<Model>` narrowed to animal/event for inspection. Resolve type
IDs and translations first; measurement meaning/unit comes from its type, not
the bare number. Dates come from the event.

For explicitly requested writes, introspect `Input_CreateData_<Model>` or
update input and connect existing animal/event/type/file records. Keep those
relations consistent on updates too. Uploading bytes and creating AnimalFile
are separate actions: an uploaded File is not automatically attached to the
event.

See [Upload a file](../../upload-file.md), [Open a file](../../open-file.md)
and [Events](../animal-events.md). No file upload or attachment is authorized
by a read-only inspection.
