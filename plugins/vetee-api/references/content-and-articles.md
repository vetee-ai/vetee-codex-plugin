# Content and articles

`Content` stores editorial content grouped by `contentCategory`.
Articles and podcasts are category variants of the same model. Inspect with
`getListContent` / `getOneContent`.

| Data | Administrative meaning |
| --- | --- |
| `code`, category, `duration` | Stable editorial identity/type and optional duration. |
| `isActive`, `publicFrom/Till` | Activation/publication configuration. |
| `isPromo`, `isPremiumOnly` | Promotion/premium flags, separate from localized text. |
| `translations` | Locale-specific slug, name, body, premium body and cover. |
| Locale/country/species filters | Audience join rows. |
| Partner/tariff filters and enable flags | Conditional access targeting. |
| `contentFiles`, `contentIndexes`, `contentLabels` | Attachments, destinations and labels. |
| `contentUsers` | Per-user read evidence. |

For title search filter `translations: {some: {name: {contains: $term,
mode: insensitive}}}`. For category use
`contentCategory: {code: {equals: "article"}}`.
Read publication/targeting explicitly; admin listing is not a customer preview.

- [Podcasts](content-and-articles/podcasts.md)
- [Markdown, translations and media](content-and-articles/content-markdown-and-media.md)

See [shared conventions](reference-data/filters-and-translations.md).
