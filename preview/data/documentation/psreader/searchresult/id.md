<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchResult/id",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12SearchResultV2id10Foundation4UUIDVvp"
  },
  "title" : "id"
}
-->

# id

A locally generated unique identifier for this result.

```
let id: UUID
```

## Discussion

This is **not** provided by the backend — it is assigned client-side on
decoding. It is used for `Hashable` and `Equatable` conformance, making
`SearchResult` suitable for use as a diffable data source item identifier
or a SwiftUI `ForEach` identity.