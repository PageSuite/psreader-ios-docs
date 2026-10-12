<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchResult/publicationName",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12SearchResultV15publicationNameSSSgvp"
  },
  "title" : "publicationName"
}
-->

# publicationName

The publication name, populated client-side by matching [`applicationId`](/documentation/PSReader/SearchResult/applicationId)
against the list of [`SearchPublication`](/documentation/PSReader/SearchPublication) entries.

```
var publicationName: String?
```

## Discussion

This is not provided by the backend — it is set after decoding by matching
the result’s [`applicationId`](/documentation/PSReader/SearchResult/applicationId) to a known publication.