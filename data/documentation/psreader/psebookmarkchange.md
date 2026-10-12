<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkChange",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17PSEBookmarkChangeO"
  },
  "title" : "PSEBookmarkChange"
}
-->

# PSEBookmarkChange

The outcome of toggling or setting a bookmark.

```
enum PSEBookmarkChange
```

## Topics

### Changes

[`PSEBookmarkChange.added(_:)`](/documentation/PSReader/PSEBookmarkChange/added(_:))

The item is now bookmarked; carries the new bookmark.

[`PSEBookmarkChange.removed(_:)`](/documentation/PSReader/PSEBookmarkChange/removed(_:))

The item’s bookmark was removed; carries the removed bookmark.

### Reading the Result

[`isBookmarked`](/documentation/PSReader/PSEBookmarkChange/isBookmarked)

True when the change left the item bookmarked.

