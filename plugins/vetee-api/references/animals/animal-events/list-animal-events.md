# List animal events

Use `getListAnimalEvent` filtered by
`animal: {id: {equals: $animalId}}`, with an explicit date range or
`animalEventType` when relevant. Order by `occurredAt` and paginate.
Include `deletedAt: null` for live records.

Return event ID, type/code/translations, `occurredAt`, `finishedAt`,
`isWholeDay`, `isEstimatedDate` and requested attached-data IDs.
A null occurrence time means an unknown/unspecified date, not today.
Estimated and whole-day values need to remain distinguishable from exact
timestamps.

For missed-reminder diagnosis also inspect reminder settings, event type's
active/reminder flags and completion state. For recurrence inspect
`isRecurringFromFinish` and interval fields. A single recurring event record
is not the entire future schedule.

Clinical values are in attachments, e.g. `animalMeasurements`, and must be
interpreted with their own type/unit. See [Events](../animal-events.md).
