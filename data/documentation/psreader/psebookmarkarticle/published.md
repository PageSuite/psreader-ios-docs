<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkArticle/published",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEBookmarkArticle(py)published"
  },
  "title" : "published"
}
-->

# published

The catalog entry of the edition the article was saved from.

```
@objc var published: PSEPublished?
```

## Discussion

[`editionSource(mode:among:onProgress:)`](/documentation/PSReader/PSEBookmark/editionSource(mode:among:onProgress:)) uses it to
reopen that edition at the article’s page.