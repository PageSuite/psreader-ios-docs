<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReplicaSearchService",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ReplicaSearchServiceC"
  },
  "title" : "ReplicaSearchService"
}
-->

# ReplicaSearchService

A [`SearchService`](/documentation/PSReader/SearchService) for searching legacy replica edition content.

```
class ReplicaSearchService
```

## Overview

`ReplicaSearchService` targets the legacy search endpoint, which indexes the
text of replica edition pages. It only returns page results — results are
typed `"REPLICA_PAGE"` — and only supports searching a single publication
per request: the first entry in the `publications` array is searched and
the rest are ignored.

The legacy endpoint is keyed by edition rather than publication, so each
search first resolves the publication to its latest edition and then
searches with publication scope. Resolved editions are cached per service
instance.

## Topics

### Creating a Search Service

[`init(session:)`](/documentation/PSReader/ReplicaSearchService/init(session:))

Creates a new replica search service.

### Searching

[`search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)`](/documentation/PSReader/ReplicaSearchService/search(accountGuid:query:type:publications:offset:limit:timeZone:completion:))

Searches for pages within the first of the specified publications.

[`search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)`](/documentation/PSReader/ReplicaSearchService/search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:))

Searches for pages within a date range.

### Errors

[`ReplicaSearchService.SearchError`](/documentation/PSReader/ReplicaSearchService/SearchError)

Errors that can occur during a replica search request.

