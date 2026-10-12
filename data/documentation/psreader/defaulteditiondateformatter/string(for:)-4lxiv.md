<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-4lxiv",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultEditionDateFormatterV6string3forSSAA15PSEBookmarkPageC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Formats the bookmarked edition’s [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) with
[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter), falling back to its [`datePublished`](/documentation/PSReader/PSEPublished/datePublished)
and then to the bookmark’s own [`editionDate`](/documentation/PSReader/PSEBookmarkPage/editionDate).

```
func string(for bookmark: PSReader.PSEBookmarkPage) -> String
```

## Parameters

`bookmark`

The bookmarked page to format.

## Return Value

A formatted string for the bookmarked page, or `"-"` if no date is available.