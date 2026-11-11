# Animal events

`AnimalEvent` is a dated record/planned activity linked to `animal` and
`animalEventType`. It carries nullable `occurredAt`, `finishedAt`,
`isWholeDay`, `isEstimatedDate`, description, reminder and recurrence settings.

`isReminderEnabled` uses `reminderUnit/Value`; `isRecurring` uses
`recurrenceUnit/Value` and `isRecurringFromFinish`. Change reminder/recurrence
settings only when explicitly requested; confirm supported values for the
selected event type.

`AnimalEventType` is translated configuration with reminder capability,
quick-action and expected attached-data flags, plus gender/species targeting.
Those flags describe what data is expected for that event type; actual data is
stored in separate typed records.

- [List and diagnose events](animal-events/list-animal-events.md)
- [Create or edit an event](animal-events/create-an-animal-event.md)
- [Files, identifications, measurements and medication](animal-events/attach-data-to-an-animal-event.md)

See [Animals](../animals.md).
