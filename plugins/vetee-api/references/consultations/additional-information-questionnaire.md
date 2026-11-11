# Additional-information questionnaire

Reusable question configuration is separate from a thread/message's answers.

| Model | Meaning |
| --- | --- |
| `AnimalThreadInformationQuestion` | Type, optional category, prompt, image, active flag and order. |
| `AnimalThreadInformationQuestionTranslation` | Localized name, description and unit. |
| `AnimalThreadInformationQuestionOption` | Configured option with translations. |
| `AnimalThreadInformation` | Requested/answered information for a thread/message/question. |

Question types: `text`, `number`, `date`, `options`.
Answer statuses: `pending`, `skipped`, `answered`. Editing shared question
configuration can change how historical data is interpreted; establish scope
before a requested change.

- [Inspect pending information](additional-information-questionnaire/fetch-pending-questions.md)
- [Stored values and corrections](additional-information-questionnaire/answer-and-confirm-questions.md)

Read question definitions separately from recorded values.
See [Consultations](../consultations.md).
