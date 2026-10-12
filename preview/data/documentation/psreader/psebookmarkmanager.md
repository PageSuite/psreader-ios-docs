<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkManager",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkManagerC"
  },
  "title" : "PSEBookmarkManager"
}
-->

# PSEBookmarkManager

Saves and restores the user’s article and page bookmarks.

```
class PSEBookmarkManager
```

## Overview

Use the [`shared`](/documentation/PSReader/PSEBookmarkManager/shared) singleton. Bookmark from reader state with
[`toggleBookmark(context:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(context:edition:published:application:)) (get the
context from [`bookmarkContext()`](/documentation/PSReader/PSEPage/bookmarkContext())), list saved items via
[`bookmarks`](/documentation/PSReader/PSEBookmarkManager/bookmarks), and open one with
[`editionSource(mode:among:onProgress:)`](/documentation/PSReader/PSEBookmark/editionSource(mode:among:onProgress:)).

Changes can be observed three ways: a [`PSEBookmarkObserver`](/documentation/PSReader/PSEBookmarkObserver) for typed
per-event callbacks, the [`bookmarksDidChange`](/documentation/PSReader/PSEBookmarkManager/bookmarksDidChange) notification for a
coarse signal, or `ObservableObject` conformance for SwiftUI. Apps
migrating pages saved with the legacy SDK should call
[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)) once at startup.

To build a bookmark button and a bookmarks list on it, see
[Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button).

## Topics

### Getting the Manager

[`shared`](/documentation/PSReader/PSEBookmarkManager/shared)

The bookmark manager. Use from the main thread.

### Bookmarking From the Reader

[`PSEBookmarkManager.BookmarkContext`](/documentation/PSReader/PSEBookmarkManager/BookmarkContext)

What a page offers for bookmarking: its single article, the page
itself, or nothing.

[`isBookmarked(context:)`](/documentation/PSReader/PSEBookmarkManager/isBookmarked(context:))

Whether the context’s article or page is bookmarked. `false` for
[`PSEBookmarkManager.BookmarkContext.none`](/documentation/PSReader/PSEBookmarkManager/BookmarkContext/none).

[`isBookmarked(spread:)`](/documentation/PSReader/PSEBookmarkManager/isBookmarked(spread:))

The spread’s bookmark state, or nil when it holds no bookmarkable
pages (e.g. an advert-only spread). True only when every
bookmarkable page in the spread is bookmarked.

[`toggleBookmark(context:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(context:edition:published:application:))

Toggles the bookmark for whatever the context holds; returns `nil`
for [`PSEBookmarkManager.BookmarkContext.none`](/documentation/PSReader/PSEBookmarkManager/BookmarkContext/none). See
[`toggleBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:)) for
the parameters.

[`PSEBookmarkChange`](/documentation/PSReader/PSEBookmarkChange)

The outcome of toggling or setting a bookmark.

### Bookmarking Articles

[`isBookmarked(article:)`](/documentation/PSReader/PSEBookmarkManager/isBookmarked(article:))

Whether the article is bookmarked.

[`bookmark(forArticle:)`](/documentation/PSReader/PSEBookmarkManager/bookmark(forArticle:))

The saved bookmark for an article, or `nil` if it isn’t bookmarked.

[`toggleBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:))

Bookmarks the article, or removes its bookmark if one exists.

[`addBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/addBookmark(forArticle:in:edition:published:application:))

Bookmarks the article, replacing any existing bookmark for it. See
[`toggleBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:)) for
the parameters.

[`removeBookmark(forArticle:page:)`](/documentation/PSReader/PSEBookmarkManager/removeBookmark(forArticle:page:))

Removes the article’s bookmark and its cached content. No effect if
it isn’t bookmarked.

### Bookmarking Pages

[`isBookmarked(page:)`](/documentation/PSReader/PSEBookmarkManager/isBookmarked(page:))

Whether the page is bookmarked.

[`bookmark(forPage:)`](/documentation/PSReader/PSEBookmarkManager/bookmark(forPage:))

The saved bookmark for a page, or `nil` if it isn’t bookmarked.

[`toggleBookmark(forPage:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forPage:edition:published:application:))

Bookmarks the page, or removes its bookmark if one exists. See
[`toggleBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:)) for
the parameters.

[`addBookmark(forPage:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/addBookmark(forPage:edition:published:application:))

Bookmarks the page, replacing any existing bookmark for it.

[`removeBookmark(forPage:)`](/documentation/PSReader/PSEBookmarkManager/removeBookmark(forPage:))

Removes the page’s bookmark and its cached content. No effect if it
isn’t bookmarked.

### Listing Saved Bookmarks

[`bookmarks`](/documentation/PSReader/PSEBookmarkManager/bookmarks)

All saved bookmarks — article bookmarks followed by page bookmarks.

[`articleBookmarks`](/documentation/PSReader/PSEBookmarkManager/articleBookmarks)

The saved article bookmarks, most recently added first.

[`pageBookmarks`](/documentation/PSReader/PSEBookmarkManager/pageBookmarks)

The saved page bookmarks, most recently added first.

[`hasBookmarks`](/documentation/PSReader/PSEBookmarkManager/hasBookmarks)

Whether any bookmarks (article or page) are saved.

### Removing Saved Bookmarks

[`removeBookmark(_:)`](/documentation/PSReader/PSEBookmarkManager/removeBookmark(_:)-5vc38)

Removes a saved bookmark of either kind.

[`removeBookmark(_:page:)`](/documentation/PSReader/PSEBookmarkManager/removeBookmark(_:page:))

Removes a saved article bookmark.

[`removeBookmark(_:)`](/documentation/PSReader/PSEBookmarkManager/removeBookmark(_:)-7ae9a)

Removes a saved page bookmark.

[`removeAllBookmarks()`](/documentation/PSReader/PSEBookmarkManager/removeAllBookmarks())

Removes every article and page bookmark.

### Observing Bookmarks

[`addObserver(_:)`](/documentation/PSReader/PSEBookmarkManager/addObserver(_:))

Starts delivering bookmark events to the observer. Observers are
held weakly.

[`removeObserver(_:)`](/documentation/PSReader/PSEBookmarkManager/removeObserver(_:))

Stops delivering bookmark events to the observer.

[`bookmarksDidChange`](/documentation/PSReader/PSEBookmarkManager/bookmarksDidChange)

Posted after any bookmark is added or removed.

### Migrating From the Legacy SDK

[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:))

One-shot, idempotent. Converts every legacy saved page into a bridged page
bookmark: identity from the legacy `.dat`, best-effort thumbnail copy into the
shared saved-bookmarks folder (the cell falls back to the remote legacy image
when absent). Opening resolves lazily through `PSLegacyBridgedEdition`.

