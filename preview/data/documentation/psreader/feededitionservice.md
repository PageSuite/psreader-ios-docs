<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV"
  },
  "title" : "FeedEditionService"
}
-->

# FeedEditionService

Fetches catalogs and content of editions on PageSuite’s current system
for an account.

```
struct FeedEditionService
```

## Overview

List a publication’s editions with it, find the latest one, or resolve
an edition from its GUID. To build an archive screen on it, see
[Fetching the Archive](/documentation/PSReader/Fetching-the-Archive).

## Topics

### Creating a Service

[`init(accountGUID:timeZone:)`](/documentation/PSReader/FeedEditionService/init(accountGUID:timeZone:))

Creates an edition service for an account.

[`accountGUID`](/documentation/PSReader/FeedEditionService/accountGUID)

The account the service’s requests are scoped to.

[`timeZone`](/documentation/PSReader/FeedEditionService/timeZone)

The time zone the service formats edition date strings in.

### Fetching the Catalog

[`publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:)`](/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:))

Returns the published-edition catalog for a publication, grouped
by date (newest first).

[`latestEdition(publicationGUID:publicationName:publishedDomain:)`](/documentation/PSReader/FeedEditionService/latestEdition(publicationGUID:publicationName:publishedDomain:))

Returns the most recently published edition for a publication.

### Archive Helpers

[`latestEdition`](/documentation/PSReader/Swift/Array/latestEdition)

The most recently published edition, or `nil` if the archive is empty.

### Browsing by Date

[`publishedEditions(publicationGUID:publicationName:startDate:endDate:pageNumber:pageSize:)`](/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:startDate:endDate:pageNumber:pageSize:))

Returns one page of a publication’s published editions between
two calendar days, grouped by date (newest first).

[`FeedEditionService.PublishedEditionsPage`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage)

One page of a date-range request.

### Resolving an Edition

[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:))

Resolves a published edition directly from an edition GUID.

[`edition(for:)`](/documentation/PSReader/FeedEditionService/edition(for:))

Loads the full content of a published edition, including its
templates. For reading, present the edition through the SDK’s reader
view controllers rather than consuming this directly.

### Errors

[`FeedEditionServiceError`](/documentation/PSReader/FeedEditionServiceError)

Errors thrown by [`FeedEditionService`](/documentation/PSReader/FeedEditionService).

