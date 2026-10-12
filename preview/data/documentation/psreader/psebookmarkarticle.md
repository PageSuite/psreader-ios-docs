<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkArticle",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEBookmarkArticle"
  },
  "title" : "PSEBookmarkArticle"
}
-->

# PSEBookmarkArticle

A persisted article bookmark, carrying the article and its origin so a bookmarks edition can rebuild it offline.

```
@objc class PSEBookmarkArticle
```

## Topics

### Showing a List Row

[`article`](/documentation/PSReader/PSEBookmarkArticle/article)

The saved article, with its headline, byline, text and images.

[`localThumbnailURL()`](/documentation/PSReader/PSEBookmarkArticle/localThumbnailURL())

The locally cached thumbnail for the bookmarked article, if present:
the first of the article’s images found in the shared saved-bookmarks
cache or in the origin edition’s cache. Populated by the caching that
runs when the bookmark is created.

[`remoteThumbnailURL()`](/documentation/PSReader/PSEBookmarkArticle/remoteThumbnailURL())

The remote URL of the article’s lead image — the thumbnail fallback
when no local copy exists.

[`editionName`](/documentation/PSReader/PSEBookmarkArticle/editionName)

The name of the edition the article was saved from.

[`bookmarkDate`](/documentation/PSReader/PSEBookmarkArticle/bookmarkDate)

The edition’s date as display text, copied from the edition when the
article was bookmarked.

[`bookmarkLogo`](/documentation/PSReader/PSEBookmarkArticle/bookmarkLogo)

The publication’s header logo for the edition’s date, as set in the
app configuration.

[`section`](/documentation/PSReader/PSEBookmarkArticle/section)

The section the article was saved from, copied from the page’s
[`section`](/documentation/PSReader/PSEPage/section).

[`sectionColor`](/documentation/PSReader/PSEBookmarkArticle/sectionColor)

The theme color of the article’s section, copied from the page’s
[`sectionColor`](/documentation/PSReader/PSEPage/sectionColor).

[`dateAdded`](/documentation/PSReader/PSEBookmarkArticle/dateAdded)

When the article was bookmarked.

### Source Edition

[`published`](/documentation/PSReader/PSEBookmarkArticle/published)

The catalog entry of the edition the article was saved from.

[`editionGUID`](/documentation/PSReader/PSEBookmarkArticle/editionGUID)

The GUID of the edition the article was saved from.

[`editionDate`](/documentation/PSReader/PSEBookmarkArticle/editionDate)

The publication date of the edition the article was saved from.

[`pageGUID`](/documentation/PSReader/PSEBookmarkArticle/pageGUID)

The GUID of the page the article was saved from.

