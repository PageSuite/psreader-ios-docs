<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchResult/parsedEditionDate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12SearchResultV17parsedEditionDate10Foundation0F0VSgvp"
  },
  "title" : "parsedEditionDate"
}
-->

# parsedEditionDate

The [`editionDate`](/documentation/PSReader/SearchResult/editionDate) parsed as a `Date`.

```
var parsedEditionDate: Date? { get }
```

## Discussion

Supports ISO 8601 timestamps with or without fractional seconds.
Returns `nil` if [`editionDate`](/documentation/PSReader/SearchResult/editionDate) is `nil` or cannot be parsed.