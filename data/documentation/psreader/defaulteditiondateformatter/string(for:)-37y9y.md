<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-37y9y",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultEditionDateFormatterV6string3forSSAA17PSBookmarkArticleC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Formats the bookmark’s edition date with [`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter).

```
func string(for bookmark: PSReader.PSBookmarkArticle) -> String
```

## Parameters

`bookmark`

The bookmarked legacy replica article to format.

## Return Value

A formatted string for the bookmarked article, or `"-"` if no date is available.