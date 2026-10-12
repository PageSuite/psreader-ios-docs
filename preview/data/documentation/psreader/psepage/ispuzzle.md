<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/isPuzzle",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)isPuzzle"
  },
  "title" : "isPuzzle"
}
-->

# isPuzzle

Whether the page is a puzzle page.

```
@objc var isPuzzle: Bool
```

## Discussion

Templated article pages can instead flag individual articles
(`PSEArticle.isPuzzle`), so check the page’s [`articles`](/documentation/PSReader/PSEPage/articles) too.