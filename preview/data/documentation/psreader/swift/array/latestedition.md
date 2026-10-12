<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Swift/Array/latestEdition",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader",
      "Swift"
    ],
    "preciseIdentifier" : "s:Sa8PSReaderAA16PSEPublishedDateCRszlE13latestEditionAA0B0CSgvp"
  },
  "title" : "latestEdition"
}
-->

# latestEdition

The most recently published edition, or `nil` if the archive is empty.

```
var latestEdition: PSEPublished? { get }
```

## Discussion

Expects the newest-first ordering returned by
[`publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:)`](/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:)).