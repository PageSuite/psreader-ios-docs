<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmark",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader11PSEBookmarkO"
  },
  "title" : "PSEBookmark"
}
-->

# PSEBookmark

A saved bookmark: either an article or a whole page.

```
enum PSEBookmark
```

## Overview

Bookmarks persist across sessions and carry enough of their content to
rebuild it offline in a [`PSEBookmarksEdition`](/documentation/PSReader/PSEBookmarksEdition). Open one with
[`editionSource(mode:among:onProgress:)`](/documentation/PSReader/PSEBookmark/editionSource(mode:among:onProgress:)).

## Topics

### Bookmark Kinds

[`PSEBookmark.article(_:)`](/documentation/PSReader/PSEBookmark/article(_:))

A saved article.

[`PSEBookmark.page(_:)`](/documentation/PSReader/PSEBookmark/page(_:))

A saved page.

### Source Edition

[`published`](/documentation/PSReader/PSEBookmark/published)

The catalog entry of the edition the bookmark came from, when known.

[`pageGUID`](/documentation/PSReader/PSEBookmark/pageGUID)

The GUID of the page this bookmark points at, if any.

### Opening a Bookmark

[`editionSource(mode:onProgress:)`](/documentation/PSReader/PSEBookmark/editionSource(mode:onProgress:))

Convenience overload that opens against all currently saved bookmarks.

[`editionSource(mode:among:onProgress:)`](/documentation/PSReader/PSEBookmark/editionSource(mode:among:onProgress:))

Resolves an edition source and opening page for this bookmark.

### Sharing

[`shareEdition`](/documentation/PSReader/PSEBookmark/shareEdition)

A minimal edition wrapper for the bookmark’s origin, suitable for
building share content.

