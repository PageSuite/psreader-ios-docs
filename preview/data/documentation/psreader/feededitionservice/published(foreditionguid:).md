<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/published(forEditionGUID:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV9published03forC4GUIDAA12PSEPublishedCSS_tYaKF"
  },
  "title" : "published(forEditionGUID:)"
}
-->

# published(forEditionGUID:)

Resolves a published edition directly from an edition GUID.

```
func published(forEditionGUID editionGUID: String) async throws -> PSEPublished
```

## Parameters

`editionGUID`

The edition GUID.

## Return Value

The edition’s catalog entry.

## Discussion

Use this when an edition identifier is all you hold — a search
result or a deep link — and the edition may be older than the
archive window
[`publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:)`](/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:))
returns. The result is ready for
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)).

The entry carries less than one from the catalog: its
[`publicationName`](/documentation/PSReader/PSEPublished/publicationName) and [`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID)
are empty. Set `publicationName` yourself when you know it.

An edition published more than once has a catalog entry for each
publish, each with its own [`publishedGUID`](/documentation/PSReader/PSEPublished/publishedGUID). This
returns one of them, which may not be the one the catalog lists
first.

> Throws: ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionServiceError/editionNotFound`` when the backend
> has no published edition with that GUID,
> ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionServiceError/invalidResponse`` when it sends something
> the service can’t read, or the underlying transport error.