<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EditionDateFormatter/string(for:)-8s11v",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20EditionDateFormatterP6string3forSSAA12SearchResultV_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Provides a formatted string representation for the given search result’s edition date.

```
func string(for result: SearchResult) -> String
```

## Parameters

`result`

The `SearchResult` to format.

## Return Value

A formatted string for the edition date, or `"-"` if the date is unavailable.