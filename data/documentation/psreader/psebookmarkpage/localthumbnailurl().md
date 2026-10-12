<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkPage/localThumbnailURL()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PSEBookmarkPageC17localThumbnailURL10Foundation0F0VSgyF"
  },
  "title" : "localThumbnailURL()"
}
-->

# localThumbnailURL()

The locally cached page screenshot in the shared saved-bookmarks folder, if
present. Populated for normal bookmarks by `cacheBookmarked(page:)` and for
bridged bookmarks by the page migration; the Saved cell prefers it.

```
func localThumbnailURL() -> URL?
```