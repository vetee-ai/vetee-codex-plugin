# Consultation category and intake configuration

`AnimalThreadCategory` configures the service, rather than an individual
question. Inspect `code`, `type` (`paid`, `free`, `limit`), `order`,
`color`, `isActive`, publication dates, translations, partner relations,
veterinarian assignments and limit/age settings. Discover exact limit fields
through the selected environment's schema.

`AnimalThreadCategoryProduct` associates recommendations/products with a
category and has locale, country, gender and species targeting. Assignments
and targeting are separate joins; translating a category does not configure
product eligibility.

Read the thread's category and compare configuration with observed status.
A later category edit does not establish the configuration at thread creation.
For requested edits resolve the category and each related ID, preserving
unrelated translations, assignments and filters.

This retains only administrative information from the source intake page;
customer question submission is omitted.
See [Consultations](../consultations.md) and
[shared conventions](../reference-data/filters-and-translations.md).
