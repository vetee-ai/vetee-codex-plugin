# Messages, read evidence and evaluations

Read `AnimalThread.animalThreadMessages` or `getListAnimalThreadMessage`
with `animalThread: {id: {equals: $threadId}}`. Order chronologically and
paginate; the first record is not inherently the latest.

`AnimalThreadMessage` links thread, user/veterinarian, optional order/LLM
record, locale information, files, indexes, products, questionnaire information
and user read/evaluation records. `message` is the base text;
`translations {id message locale {id code}}` contains localized text.

Types: `user`, `llm`, `llmProposal`, `shop`, `veterinarian`.
Message statuses: `pending`, `processing`, `done`. A completed LLM message
is not a final veterinarian answer; inspect type, author and thread status.

Read/evaluation joins are per user, not a single thread-wide read flag.
Inspect their live fields and user relation; do not log reads during audits.
Evaluation values include `positive`, `negative` and a `useful*` scale;
do not reduce all values to one boolean.

For requested text corrections target the exact message/translation ID.
Sending customer messages and marking reads are omitted.
See [Consultations](../consultations.md).
