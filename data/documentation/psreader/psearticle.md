<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEArticle",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEArticle"
  },
  "title" : "PSEArticle"
}
-->

# PSEArticle

An editorial article, with its text, imagery, and metadata.

```
@objc class PSEArticle
```

## Overview

Articles arrive on the [`PSEPage`](/documentation/PSReader/PSEPage)s that present them ([`articles`](/documentation/PSReader/PSEPage/articles))
and grouped under their [`PSESection`](/documentation/PSReader/PSESection). Property names mirror the backend
payload and are part of the shipped contract, casing included (note
[`articleguid`](/documentation/PSReader/PSEArticle/articleguid), [`sharelink`](/documentation/PSReader/PSEArticle/sharelink)).

For how the catalog and content models fit together, see
[The Edition Model](/documentation/PSReader/The-Edition-Model).

## Topics

### Identity

[`articleguid`](/documentation/PSReader/PSEArticle/articleguid)

Unique identifier of the article (lowercase by contract).

[`uniqueid`](/documentation/PSReader/PSEArticle/uniqueid)

A unique identifier for the article, as sent by the backend.

[`GUID`](/documentation/PSReader/PSEArticle/GUID-4mj0i)

The identifier of the source feed item the article came from, as sent
by the backend under `GUID`.

[`guid`](/documentation/PSReader/PSEArticle/guid-2c2ks)

The identifier of the source feed item the article came from, as sent
by the backend under `guid`.

### Section

[`section`](/documentation/PSReader/PSEArticle/section)

Name of the section the article appears under.

[`sectioncolor`](/documentation/PSReader/PSEArticle/sectioncolor)

The color of the article’s section, as the red, green and blue
components that the reader inserts into CSS `rgb()`.

### Text

[`headline`](/documentation/PSReader/PSEArticle/headline)

The article’s headline.

[`shortHeadline`](/documentation/PSReader/PSEArticle/shortHeadline)

A shortened headline for constrained layouts.

[`subheadline`](/documentation/PSReader/PSEArticle/subheadline)

The article’s subheadline.

[`shortDescription`](/documentation/PSReader/PSEArticle/shortDescription)

A brief standfirst or summary.

[`label`](/documentation/PSReader/PSEArticle/label)

A short display label for the article, as sent by the backend.

[`story`](/documentation/PSReader/PSEArticle/story)

The article’s body as HTML. (The old Core SDK called this `body`.)

[`keywords`](/documentation/PSReader/PSEArticle/keywords)

Editorial keywords attached to the article.

[`category`](/documentation/PSReader/PSEArticle/category)

The article’s category, as sent by the backend.

[`datecreated`](/documentation/PSReader/PSEArticle/datecreated)

When the article was created, as a date string from the backend.

### Byline

[`author`](/documentation/PSReader/PSEArticle/author)

The author’s name.

[`byline`](/documentation/PSReader/PSEArticle/byline)

The article’s byline as plain text.

[`bylineHTML`](/documentation/PSReader/PSEArticle/bylineHTML)

Byline as HTML for template rendering. Authors that have an email are wrapped in a
`<a href="mailto:…">` so the article template’s `.author a` rule colors them; authors
without an email stay as plain text. `byline`/`author` remain plain text for analytics,
audio, bookmarks and TTS — only this property carries markup.

[`authorCredit`](/documentation/PSReader/PSEArticle/authorCredit)

The author’s credit line, when the backend sends one.

[`authorEmail`](/documentation/PSReader/PSEArticle/authorEmail)

The author’s email address, when the backend sends one.

[`bylineimageurl`](/documentation/PSReader/PSEArticle/bylineimageurl)

URL of an image to show with the byline, when the backend sends one.

### Article Kind

[`isPuzzle`](/documentation/PSReader/PSEArticle/isPuzzle)

Whether the backend marks the article as a puzzle.

[`isComic`](/documentation/PSReader/PSEArticle/isComic)

Whether the backend marks the article as a comic.

### Media

[`leadAsset()`](/documentation/PSReader/PSEArticle/leadAsset())

The article’s lead asset: its flagged lead video or image, else its
first image or video, else the article-level landscape image.

[`images`](/documentation/PSReader/PSEArticle/images)

The article’s images with their crops and captions.

[`videos`](/documentation/PSReader/PSEArticle/videos)

Videos embedded in the article.

[`mediaObjects`](/documentation/PSReader/PSEArticle/mediaObjects)

Media objects embedded in the article, such as videos and image
galleries.

[`imageLandscape`](/documentation/PSReader/PSEArticle/imageLandscape)

Landscape image URL supplied at the article level in the feed (`imagelandscape`).
Used as a fallback lead image when an article has no images or videos.

[`imageLandscapeCaption`](/documentation/PSReader/PSEArticle/imageLandscapeCaption)

Caption for the fallback landscape image, sourced from `cmsMetadata.payload.image.caption`.

[`imageLandscapeCredit`](/documentation/PSReader/PSEArticle/imageLandscapeCredit)

Credit for the fallback landscape image, sourced from `cmsMetadata.payload.image.credit`.

[`alternativeImageUrl`](/documentation/PSReader/PSEArticle/alternativeImageUrl)

URL of an alternative image for the article, when the backend sends
one.

[`PSEMedia`](/documentation/PSReader/PSEMedia)

One media asset on a page: an article’s image or video, or an advert.

[`PSEImage`](/documentation/PSReader/PSEImage)

An article image with its crops, caption, and credit.

[`PSEImageCrops`](/documentation/PSReader/PSEImageCrops)

The set of crop variants available for an image.

[`PSEImageCrop`](/documentation/PSReader/PSEImageCrop)

One crop variant of an image.

[`PSEVideo`](/documentation/PSReader/PSEVideo)

A video embedded in an article.

### Adverts

[`adverts`](/documentation/PSReader/PSEArticle/adverts)

In-article advert slots.

### Sharing

[`sharelink`](/documentation/PSReader/PSEArticle/sharelink)

Public web URL for sharing the article.

### Metadata

[`metadata`](/documentation/PSReader/PSEArticle/metadata)

Additional article metadata, such as commenting identifiers. `nil`
when the backend sends none.

[`PSEArticleMetadata`](/documentation/PSReader/PSEArticleMetadata)

Article-level metadata, including commenting identifiers.

[`PSECoralCommenting`](/documentation/PSReader/PSECoralCommenting)

Coral commenting identifiers for an article.

