<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarksEdition",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEBookmarksEditionV"
  },
  "title" : "PSEBookmarksEdition"
}
-->

# PSEBookmarksEdition

An edition source synthesized from saved bookmarks: one page per
bookmark, readable offline.

```
struct PSEBookmarksEdition
```

## Overview

This is the fallback the prebuilt UI uses when a bookmark’s original
edition can’t be opened (not downloaded and no connection). Build one
from any bookmark set — for example a single feed’s saved articles —
or let [`editionSource(mode:onProgress:)`](/documentation/PSReader/PSEBookmark/editionSource(mode:onProgress:)) construct it
for you.

## Topics

### Creating a Bookmarks Edition

[`init(bookmarks:)`](/documentation/PSReader/PSEBookmarksEdition/init(bookmarks:))

Builds a bookmarks edition from a bookmark set. Bookmarks that
cannot produce a page are skipped.

### Content

[`edition`](/documentation/PSReader/PSEBookmarksEdition/edition)

The synthesized edition: one page per bookmark, in the order of
[`bookmarks`](/documentation/PSReader/PSEBookmarksEdition/bookmarks), each in its own single-page spread.

[`published`](/documentation/PSReader/PSEBookmarksEdition/published)

A placeholder catalog entry shared by every bookmarks edition.

[`bookmarks`](/documentation/PSReader/PSEBookmarksEdition/bookmarks)

The bookmarks that produced a page, in the same order as
`edition.pages` (bookmarks that yield no page are dropped).

[`page(for:)`](/documentation/PSReader/PSEBookmarksEdition/page(for:))

The synthesized page representing `bookmark`, or nil if it isn’t in
this edition.

