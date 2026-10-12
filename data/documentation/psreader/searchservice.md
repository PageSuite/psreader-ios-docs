<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchService",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13SearchServiceP"
  },
  "title" : "SearchService"
}
-->

# SearchService

A service for searching PageSuite edition content.

```
protocol SearchService
```

## Overview

The SDK provides two implementations, one per backend:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedSearchService`` searches editions on PageSuite’s current system via
  the PageSuite search API.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ReplicaSearchService`` searches legacy replica editions via the legacy
  search endpoint.

A client is wholly on one backend — the two are never mixed at runtime.
The SDK’s search UI picks the implementation from the type of the first
[`SearchPublication`](/documentation/PSReader/SearchPublication) provided by the [`SearchDelegate`](/documentation/PSReader/SearchDelegate).

To build your own search screen, see [Building a Search Screen](/documentation/PSReader/Building-a-Search-Screen). The
prebuilt screen, [`SearchViewController`](/documentation/PSReader/SearchViewController), is covered in [Search](/documentation/PSReader/Search).

## Topics

### Searching

[`search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)`](/documentation/PSReader/SearchService/search(accountGuid:query:type:publications:offset:limit:timeZone:completion:))

Searches for content across the specified publications.

### Replica Editions

[`ReplicaSearchService`](/documentation/PSReader/ReplicaSearchService)

A [`SearchService`](/documentation/PSReader/SearchService) for searching legacy replica edition content.

