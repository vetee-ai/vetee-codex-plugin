# Consultations

`AnimalThread` links `user`, optional `animal`, `animalThreadCategory`,
`locale`, assigned `veterinarian`, messages and questionnaire information.
`type` distinguishes ordinary `consultation` from shop-linked `shopItem`.

Use `getListAnimalThread` / `getOneAnimalThread`. Useful filters include
`user`, `animal`, `veterinarian`, `animalThreadCategory`, `type`,
`status` and `deletedAt`. Read IDs/status/timestamps before requesting
message bodies or medical details.

- [Category and intake configuration](consultations/start-a-consultation.md)
- [Thread status and processing](consultations/thread-status-and-processing.md)
- [Additional-information questionnaire](consultations/additional-information-questionnaire.md)
- [Messages, read evidence and evaluations](consultations/messages-reads-and-unread-threads.md)

These pages omit consumer question submission, sending messages, payment and
answering questionnaires. Generic CRUD edits records; it does not imply the
business workflow ran. Never advance statuses to repair a queue without an
explicit request.

See [shared conventions](reference-data/filters-and-translations.md).
