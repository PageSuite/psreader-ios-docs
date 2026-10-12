<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkArticle/localThumbnailURL()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEBookmarkArticleC17localThumbnailURL10Foundation0F0VSgyF"
  },
  "title" : "localThumbnailURL()"
}
-->

# localThumbnailURL()

The locally cached thumbnail for the bookmarked article, if present:
the first of the article’s images found in the shared saved-bookmarks
cache or in the origin edition’s cache. Populated by the caching that
runs when the bookmark is created.

```
func localThumbnailURL() -> URL?
```