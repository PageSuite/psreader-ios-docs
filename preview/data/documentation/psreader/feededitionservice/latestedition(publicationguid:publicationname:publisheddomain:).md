<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/latestEdition(publicationGUID:publicationName:publishedDomain:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV06latestC015publicationGUID0F4Name15publishedDomainAA12PSEPublishedCSS_SSSgAJtYaKF"
  },
  "title" : "latestEdition(publicationGUID:publicationName:publishedDomain:)"
}
-->

# latestEdition(publicationGUID:publicationName:publishedDomain:)

Returns the most recently published edition for a publication.

```
func latestEdition(publicationGUID: String, publicationName: String? = nil, publishedDomain: String? = nil) async throws -> PSEPublished
```