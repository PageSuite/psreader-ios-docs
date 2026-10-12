<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchResult/editionDate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12SearchResultV11editionDateSSSgvp"
  },
  "title" : "editionDate"
}
-->

# editionDate

The edition date in ISO 8601 format. The backend may return this with
or without fractional seconds (`yyyy-MM-dd'T'HH:mm:ss.SSS'Z'` or
`yyyy-MM-dd'T'HH:mm:ss'Z'`). Use [`parsedEditionDate`](/documentation/PSReader/SearchResult/parsedEditionDate) to get a `Date`.

```
let editionDate: String?
```