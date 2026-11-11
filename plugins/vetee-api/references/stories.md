# Stories

A `Story` is a published promotional entry combining a destination `index`,
default thumbnail/cover, localized names/media, publication dates and audience
configuration. It is separate from `Content` articles.

Use `getListStory` / `getOneStory` for inspection:

```graphql
query InspectStories($filter: Input_Filter_Story, $pagination: Input_Pagination) {
  getListStory(filter: $filter, order: {publicFrom: asc}, pagination: $pagination) {
    status { success errorCode errorMessage }
    meta { limit offset total }
    nodes {
      id isActive deletedAt publicFrom publicTill isPremiumOnly color
      index { id type typeId url }
      translations { id name locale { id code } coverFile { id } }
    }
  }
}
```

Pass explicit pagination and filters. For active records use
`isActive: {equals: true}` and `deletedAt: null`, plus the intended dates.
Admin reads do not apply app audience restrictions. `index` describes the
destination, not the story identity; resolve its record before a requested edit.

- [Audience, translations and read records](stories/audience-and-translations.md)

See [shared conventions](reference-data/filters-and-translations.md).
