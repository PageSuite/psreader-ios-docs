<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager/BookmarkContext",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC15BookmarkContextO"
  },
  "title" : "PSEBookmarkManager.BookmarkContext"
}
-->

# PSEBookmarkManager.BookmarkContext

What a page offers for bookmarking: its single article, the page
itself, or nothing.

```
enum BookmarkContext
```

## Overview

Get one from [`bookmarkContext()`](/documentation/PSReader/PSEPage/bookmarkContext()) and feed it to the
context-based methods — this is the universal path a bookmark button
in a custom reader should use.

## Topics

### Contexts

[`PSEBookmarkManager.BookmarkContext.article(_:_:)`](/documentation/PSReader/PSEBookmarkManager/BookmarkContext/article(_:_:))

An article to bookmark, with the page that holds it.

[`PSEBookmarkManager.BookmarkContext.page(_:)`](/documentation/PSReader/PSEBookmarkManager/BookmarkContext/page(_:))

A page to bookmark as a whole.

[`PSEBookmarkManager.BookmarkContext.none`](/documentation/PSReader/PSEBookmarkManager/BookmarkContext/none)

Nothing to bookmark, as on advert pages and template pages with
more than one article.

### Checking the Context

[`isBookmarkable`](/documentation/PSReader/PSEBookmarkManager/BookmarkContext/isBookmarkable)

Whether this context can be bookmarked at all.

