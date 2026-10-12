<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkObserver",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEBookmarkObserverP"
  },
  "title" : "PSEBookmarkObserver"
}
-->

# PSEBookmarkObserver

Receives bookmark additions and removals from [`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager).

```
protocol PSEBookmarkObserver : AnyObject
```

## Overview

Every method has a no-op default, so conform to just the events you care
about. Register with [`addObserver(_:)`](/documentation/PSReader/PSEBookmarkManager/addObserver(_:)).

## Topics

### Article Bookmarks

[`bookmarkManager(articleBookmarked:)`](/documentation/PSReader/PSEBookmarkObserver/bookmarkManager(articleBookmarked:))

Called after an article is bookmarked.

[`bookmarkManager(articleBookmarkDeleted:)`](/documentation/PSReader/PSEBookmarkObserver/bookmarkManager(articleBookmarkDeleted:))

Called after an article bookmark is removed.

### Page Bookmarks

[`bookmarkManager(pageBookmarked:)`](/documentation/PSReader/PSEBookmarkObserver/bookmarkManager(pageBookmarked:))

Called after a page is bookmarked, including each page bookmark that
[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)) adds.

[`bookmarkManager(pageBookmarkDeleted:)`](/documentation/PSReader/PSEBookmarkObserver/bookmarkManager(pageBookmarkDeleted:))

Called after a page bookmark is removed.

