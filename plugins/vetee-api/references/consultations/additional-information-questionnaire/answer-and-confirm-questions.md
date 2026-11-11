# Stored questionnaire values and corrections

Inspect status and value fields alongside the question type:

- Text: `textValue`.
- Number: `numberValue`, which is a **String** in the current model/admin
  contract, not a numeric GraphQL scalar.
- Date: `dateValue`.
- Option: `animalThreadInformationQuestionOption`, belonging to the question.

Status and stored value are separate. `skipped` is not `answered`;
a non-null value alone does not establish completion. For an explicit
administrative correction, introspect the update input, verify the
question/option relationship and change only requested fields.

Generic data edits do not run customer answer/confirm transitions. Those app
flows are omitted.
See [Questionnaire](../additional-information-questionnaire.md).
