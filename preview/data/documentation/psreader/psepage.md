<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage"
  },
  "title" : "PSEPage"
}
-->

# PSEPage

A single page of an edition — a rendered PDF page, a templated HTML
article page, or a dedicated advert page.

```
@objc class PSEPage
```

## Overview

[`type`](/documentation/PSReader/PSEPage/type) discriminates what the page is (for example `replica_pdf_page`,
`templateArticle`, or the `advert*` family — see [`isAdvertPage`](/documentation/PSReader/PSEPage/isAdvertPage));
[`articles`](/documentation/PSReader/PSEPage/articles) carries the editorial content presented on the page, and
[`mediaObjects`](/documentation/PSReader/PSEPage/mediaObjects) its interactive hotspots. Property names mirror the
backend payload and are part of the shipped contract, casing included
(note [`pageguid`](/documentation/PSReader/PSEPage/pageguid)).

For how the catalog and content models fit together, see
[The Edition Model](/documentation/PSReader/The-Edition-Model).

## Topics

### Identity

[`pageguid`](/documentation/PSReader/PSEPage/pageguid)

Unique identifier of the page (lowercase by contract).

[`editionGUID`](/documentation/PSReader/PSEPage/editionGUID)

The GUID of the edition the page came from.

[`section`](/documentation/PSReader/PSEPage/section)

The section this page belongs to. This value serves as both the
section’s display name and the match key for
[`scrollTo(sectionGUID:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(sectionGUID:source:))
(compared case-insensitively).

[`sectionColor`](/documentation/PSReader/PSEPage/sectionColor)

The owning section’s theme color, as comma-separated red, green, and
blue components from 0 to 255 (for example `0,0,0`).

### Page Labels

[`pageLabel`](/documentation/PSReader/PSEPage/pageLabel)

The label every user-facing page reference shows: the friendly page
name where the feed provides one, otherwise the derived `pageNumber`.

[`friendlyPageName`](/documentation/PSReader/PSEPage/friendlyPageName)

The friendly page label to show for this page, or nil when the
edition provides none: `displayName`, else the host page’s for article pages.

[`pageNumber`](/documentation/PSReader/PSEPage/pageNumber)

The page’s printed page number.

[`feedPageNumber`](/documentation/PSReader/PSEPage/feedPageNumber)

The page number exactly as the edition’s data published it. The data
numbers advert pages as if they were printed pages, shifting every
subsequent page — `pageNumber` is normalized to the printed folio at
edition load (`PSEEdition.normalizePageNumbers`), and this preserves
the raw value for anything that must use the published numbering.
0 until normalization has run.

[`displayName`](/documentation/PSReader/PSEPage/displayName)

The publisher’s friendly page label (“A1”, “B12”…) exactly as the
edition’s data published it. Optional and opaque: it is never parsed or reformatted,
and whole editions or individual pages may lack it.

[`hostDisplayName`](/documentation/PSReader/PSEPage/hostDisplayName)

The `displayName` of the classic PDF page hosting this article-level page,
resolved at edition load (`PSEEdition.resolveHostDisplayNames`). Article
pages carry no friendly name of their own and inherit their host’s.

### Page Kind

[`type`](/documentation/PSReader/PSEPage/type)

The page kind, e.g. `replica_pdf_page`, `templateArticle`, or one of
the `advert*` variants.

[`PSEPageType`](/documentation/PSReader/PSEPageType)

The kind of content a reader screen shows: a page, article, or advert
from either edition system, or other content such as an image gallery.

[`isPDF`](/documentation/PSReader/PSEPage/isPDF)

Whether the page renders from a PDF (`replica_pdf_page` or
`page_pdf`).

[`isAdvertPage`](/documentation/PSReader/PSEPage/isAdvertPage)

True for dedicated advert pages of any kind
(`advert`, `advert_html`, `advert_pdf`, `advert_third_party`).

[`isExternal`](/documentation/PSReader/PSEPage/isExternal)

Whether the page renders externally hosted web content (its
[`external`](/documentation/PSReader/PSEPage/external) flag is set, or its [`type`](/documentation/PSReader/PSEPage/type) is `webview`).

[`external`](/documentation/PSReader/PSEPage/external)

Whether the backend flags the page as externally hosted web content,
which the reader loads from [`contenturl`](/documentation/PSReader/PSEPage/contenturl).

[`isPuzzle`](/documentation/PSReader/PSEPage/isPuzzle)

Whether the page is a puzzle page.

[`isComic`](/documentation/PSReader/PSEPage/isComic)

Whether the page is a comic page.

[`isPageZero`](/documentation/PSReader/PSEPage/isPageZero)

Whether the page sits at the page-zero position, before the cover.

[`hasResizableText`](/documentation/PSReader/PSEPage/hasResizableText)

Whether the page renders templated content whose text responds to the
reader’s text-size setting — PDF, advert and external/webview pages don’t.

[`level`](/documentation/PSReader/PSEPage/level)

The page’s flow level; article pages report `article`.

### Advert Pages

[`advertProvider`](/documentation/PSReader/PSEPage/advertProvider)

The provider serving this advert page, parsed from
[`advertType`](/documentation/PSReader/PSEPage/advertType); `nil` for non-advert pages and unknown
providers.

[`advertType`](/documentation/PSReader/PSEPage/advertType)

For advert pages, the serving provider’s raw name — see
[`advertProvider`](/documentation/PSReader/PSEPage/advertProvider).

[`advertConfig`](/documentation/PSReader/PSEPage/advertConfig)

For third-party advert pages, the advert’s configuration as
published, or `nil` when the page has none.

### Content

[`articles`](/documentation/PSReader/PSEPage/articles)

The editorial articles presented on this page.

[`mediaObjects`](/documentation/PSReader/PSEPage/mediaObjects)

The page’s interactive hotspots (links, article jumps, media).

[`PSEMediaObject`](/documentation/PSReader/PSEMediaObject)

An interactive hotspot on a page: a tappable region that links out,
jumps within the edition, or plays media.

[`media(order:)`](/documentation/PSReader/PSEPage/media(order:))

The page’s media: a lead asset first (the first one found among its
articles), then the page’s adverts, then the articles’ other images
and videos in the requested order.

[`PSMediaOrder`](/documentation/PSReader/PSMediaOrder)

The ordering applied to a page’s non-lead media in
[`media(order:)`](/documentation/PSReader/PSEPage/media(order:)).

[`adverts`](/documentation/PSReader/PSEPage/adverts)

Advert slots placed on this page.

[`puzzles`](/documentation/PSReader/PSEPage/puzzles)

Interactive puzzles hosted on this page.

[`PSEPuzzle`](/documentation/PSReader/PSEPuzzle)

An interactive puzzle hosted on a page.

### Loading the Page

[`contenturl`](/documentation/PSReader/PSEPage/contenturl)

The page’s main content: the PDF file for PDF pages, the HTML template
the reader fills in for templated pages, or the web address for
external pages (see [`isExternal`](/documentation/PSReader/PSEPage/isExternal)).

[`baseURL`](/documentation/PSReader/PSEPage/baseURL)

The base URL the page’s HTML resolves relative references against.

[`contenturlFull`](/documentation/PSReader/PSEPage/contenturlFull)

A URL for the page’s HTML, as sent by the backend.

[`contenturlOriginal`](/documentation/PSReader/PSEPage/contenturlOriginal)

A URL for the page’s original HTML, as sent by the backend.

### Images

[`effectiveScreenshotURL`](/documentation/PSReader/PSEPage/effectiveScreenshotURL)

The best screenshot URL for the page: [`screenshoturl`](/documentation/PSReader/PSEPage/screenshoturl) when set,
else derived from a PDF page’s content URL, else `nil`.

[`screenshoturl`](/documentation/PSReader/PSEPage/screenshoturl)

URL of the page’s rendered screenshot — see
[`effectiveScreenshotURL`](/documentation/PSReader/PSEPage/effectiveScreenshotURL) for the derived fallback.

[`thumbnailFullURL`](/documentation/PSReader/PSEPage/thumbnailFullURL)

URL of the page’s full-size thumbnail image.

[`highRes`](/documentation/PSReader/PSEPage/highRes)

The URL of a high-resolution image of the page, as sent by the
backend.

[`pagesInImage`](/documentation/PSReader/PSEPage/pagesInImage)

The number of images [`highRes`](/documentation/PSReader/PSEPage/highRes) spans; `1` by default.

### Page Size

[`portraitWidth`](/documentation/PSReader/PSEPage/portraitWidth)

The page’s layout width in portrait orientation, as sent by the
backend, or `nil` when the page doesn’t specify one.

[`portraitHeight`](/documentation/PSReader/PSEPage/portraitHeight)

The page’s layout height in portrait orientation, as sent by the
backend, or `nil` when the page doesn’t specify one.

[`landscapeWidth`](/documentation/PSReader/PSEPage/landscapeWidth)

The page’s layout width in landscape orientation, as sent by the
backend, or `nil` when the page doesn’t specify one.

[`landscapeHeight`](/documentation/PSReader/PSEPage/landscapeHeight)

The page’s layout height in landscape orientation, as sent by the
backend, or `nil` when the page doesn’t specify one.

[`PSEMeasurement`](/documentation/PSReader/PSEMeasurement)

A page dimension with its unit, as delivered by the backend.

### Bookmarking

[`bookmarkContext()`](/documentation/PSReader/PSEPage/bookmarkContext())

What this page offers for bookmarking: PDF and webview pages
bookmark as pages, single-article template pages bookmark as their
article, everything else is not bookmarkable.

[`bookmark`](/documentation/PSReader/PSEPage/bookmark)

The article bookmark a [`PSEBookmarksEdition`](/documentation/PSReader/PSEBookmarksEdition) built this page from,
or `nil` for pages that didn’t come from an article bookmark.

