<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/isComic",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)isComic"
  },
  "title" : "isComic"
}
-->

# isComic

Whether the page is a comic page.

```
@objc var isComic: Bool
```

## Discussion

Templated article pages can instead flag individual articles
(`PSEArticle.isComic`), so check the page’s [`articles`](/documentation/PSReader/PSEPage/articles) too.