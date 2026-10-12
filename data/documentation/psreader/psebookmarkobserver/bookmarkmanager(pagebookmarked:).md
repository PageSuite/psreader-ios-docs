<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkObserver/bookmarkManager(pageBookmarked:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEBookmarkObserverP15bookmarkManager14pageBookmarkedyAA0B4PageC_tF"
  },
  "title" : "bookmarkManager(pageBookmarked:)"
}
-->

# bookmarkManager(pageBookmarked:)

Called after a page is bookmarked, including each page bookmark that
[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)) adds.

```
func bookmarkManager(pageBookmarked bookmark: PSEBookmarkPage)
```

## Parameters

`bookmark`

The new page bookmark.