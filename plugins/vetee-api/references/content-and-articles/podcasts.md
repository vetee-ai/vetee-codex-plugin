# Podcasts

Podcasts are `Content` records whose `contentCategory.code` is `podcast`;
there is no separate Podcast model/root operation. Filter `getListContent`
by that category, and inspect `duration`, publication flags/dates, cover,
translations and media relations.

The title/body are in ContentTranslation, not a separate episode object.
Inspect the requested locale and premium body separately. Media may be
embedded in Markdown/HTML or linked through content/file joins; a cover image
does not establish the audio source.

For a requested correction use Content, the exact translation, or media join
as appropriate. Do not change the category merely to fix a localized title.
Keep audience, premium settings and publication state unless those are part
of the request.

Listening/playback and logging reads are omitted.
See [Content](../content-and-articles.md) and
[Markdown/media](content-markdown-and-media.md).
