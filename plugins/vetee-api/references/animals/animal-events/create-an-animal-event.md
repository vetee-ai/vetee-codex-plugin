# Create or edit an animal event

Only on explicit request use `createOneAnimalEvent` / `updateOneAnimalEvent`.
Inspect the input and resolve `animal` and `animalEventType` IDs.
Connect them using the confirmed relation shapes.

Set `occurredAt`, `isWholeDay`, `isEstimatedDate`, description and
completion only as requested. Use timestamps with a timezone for precise
instants. Preserve unknown dates as null when supported rather than inventing
an occurrence.

For requested reminder/recurrence changes, verify event type capability,
interval units/values and whether the interval is based on occurrence or
finish. Preserve existing settings when only recording or correcting an event.

Adding the event alone does not add its measurements, files or medications.
Read back IDs/settings and create only the requested
[attached data](attach-data-to-an-animal-event.md).
See [Events](../animal-events.md).
