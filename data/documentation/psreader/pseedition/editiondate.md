<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/editionDate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEEdition(py)editionDate"
  },
  "title" : "editionDate"
}
-->

# editionDate

The edition’s date, parsed from [`pubdate`](/documentation/PSReader/PSEEdition/pubdate).

```
@objc var editionDate: Date?
```

## Discussion

`nil` when [`pubdate`](/documentation/PSReader/PSEEdition/pubdate) is missing or isn’t an ISO 8601 UTC timestamp
such as `2026-09-01T00:00:00Z` (with or without milliseconds).