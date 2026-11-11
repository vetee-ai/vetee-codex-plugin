# Inspect pending questionnaire information

Read `AnimalThread.animalThreadInformation`, using
`status: {equals: pending}` for outstanding records. Return information IDs,
status, linked question/type, translated label/unit, option and stored values.
Include answered/skipped records when diagnosing a thread stuck in
`pendingInformation`.

Current admin fields on `AnimalThreadInformation` include
`animalThreadMessage`, `animalThreadInformationQuestion` and
`animalThreadInformationQuestionOption`; the direct `animalThread` relation
is not exposed in admin ACL. Read through the parent thread/message instead
of inventing that field in a root model filter.

Question definitions can change after answers are recorded. A missing
translation does not mean the answer is absent. This inspection does not
confirm a questionnaire or advance its thread.
See [Questionnaire](../additional-information-questionnaire.md).
