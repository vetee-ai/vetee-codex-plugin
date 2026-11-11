# Story audience and translations

`StoryTranslation` links `object` and `locale`, with `name`, `thumbnailFile`
and `coverFile`. Inspect translated and base media separately.

`StoryLocaleFilter`, `StoryCountryFilter`, `StoryAnimalSpeciesFilter`,
`StoryPartnerFilter` and `StoryOfferTariffFilter` connect a story to reference
data with `isActive`. For species targeting use
`animalSpeciesFilters: {some: {isActive: {equals: true},
animalSpecies: {code: {equals: "dog"}}}}`. Add locale/country conditions for
the requested audience. Empty collections do not match `some`.

`isPartnerFilterEnabled` and `isOfferTariffFilterEnabled` enable the respective
audience dimensions. Inspect each flag together with its configured filter
rows when changing targeting. Do not infer customer eligibility solely from
an administrative query or an empty filter collection.

`StoryUser` links `story`, `user`, `lastReadAt`. Inspect it for read
evidence; `storyUsers: {none: {user: {id: {equals: $userId}}}}` excludes
records associated with that user. Do not generate reads during an audit.

For a requested change, update only the relevant translation/join/flag.
See [shared conventions](../reference-data/filters-and-translations.md)
and [Stories](../stories.md).
