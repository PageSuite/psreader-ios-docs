<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:startDate:endDate:pageNumber:pageSize:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV17publishedEditions15publicationGUID0G4Name9startDate03endK010pageNumber0M4SizeAC09PublishedF4PageVSS_SSSgS2SS2itYaKF"
  },
  "title" : "publishedEditions(publicationGUID:publicationName:startDate:endDate:pageNumber:pageSize:)"
}
-->

# publishedEditions(publicationGUID:publicationName:startDate:endDate:pageNumber:pageSize:)

Returns one page of a publication’s published editions between
two calendar days, grouped by date (newest first).

```
func publishedEditions(publicationGUID: String, publicationName: String? = nil, startDate: String, endDate: String, pageNumber: Int = 1, pageSize: Int = 25) async throws -> PublishedEditionsPage
```

## Discussion

The request mirrors the publications API. `startDate` and `endDate`
are inclusive calendar days written `yyyy-MM-dd`, which the backend
reads in the publication’s time zone. Pages count publishing dates,
not editions, so `pageSize` is the number of [`PSEPublishedDate`](/documentation/PSReader/PSEPublishedDate)
groups per page, from 1 to 100; a calendar month always fits in one
page of 100.

```swift
let page = try await service.publishedEditions(
    publicationGUID: "PUBLICATION_GUID",
    startDate: "2026-09-01",
    endDate: "2026-09-30",
    pageSize: 100
)
```

A range without editions returns an empty page. So does a day the
backend cannot read, or an `endDate` before `startDate`.

> Throws: ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionServiceError/publicationNotFound`` for an
> unknown publication, ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionServiceError/invalidResponse``
> when the backend rejects the request, or the underlying transport
> error.