<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-5sjpw",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultEditionDateFormatterV6string3forSSAA12SearchResultV_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Formats the search result’s edition date.

```
func string(for result: SearchResult) -> String
```

## Parameters

`result`

The search result to format.

## Return Value

A formatted string for the edition date, or `"-"` if the date is unavailable.

## Discussion

Uses [`parsedEditionDate`](/documentation/PSReader/SearchResult/parsedEditionDate) to obtain the date.