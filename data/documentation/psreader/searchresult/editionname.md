<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchResult/editionName",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12SearchResultV11editionNameSSSgvp"
  },
  "title" : "editionName"
}
-->

# editionName

The edition name, populated for replica results only.

```
var editionName: String?
```

## Discussion

Replica editions carry a display name (often a formatted date) instead
of an edition date. This field is not part of the feed backend response —
it is filled in client-side by [`ReplicaSearchService`](/documentation/PSReader/ReplicaSearchService).