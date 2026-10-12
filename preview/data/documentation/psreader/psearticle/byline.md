<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEArticle/byline",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEArticle(py)byline"
  },
  "title" : "byline"
}
-->

# byline

The article’s byline as plain text.

```
@objc var byline: String?
```

## Discussion

When the backend lists several authors, the SDK joins their names as
“A and B” or “A, B and C” and sets [`author`](/documentation/PSReader/PSEArticle/author) to the same text.
[`bylineHTML`](/documentation/PSReader/PSEArticle/bylineHTML) carries the same byline with email links.