<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-2kybo",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultEditionDateFormatterV6string3forSSAA18PSEBookmarkArticleC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Formats the bookmarked edition’s [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) with
[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter), falling back to its [`datePublished`](/documentation/PSReader/PSEPublished/datePublished)
and then to the bookmark’s own [`editionDate`](/documentation/PSReader/PSEBookmarkArticle/editionDate).

```
func string(for bookmark: PSReader.PSEBookmarkArticle) -> String
```

## Parameters

`bookmark`

The bookmarked article to format.

## Return Value

A formatted string for the bookmarked article, or `"-"` if no date is available.