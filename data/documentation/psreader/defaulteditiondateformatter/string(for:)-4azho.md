<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-4azho",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultEditionDateFormatterV6string3forSSAA10PSBookmarkC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Formats the bookmark’s edition date with [`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter).

```
func string(for bookmark: PSReader.PSBookmark) -> String
```

## Parameters

`bookmark`

The bookmarked legacy replica page to format.

## Return Value

A formatted string for the bookmarked page, or `"-"` if no date is available.