<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedSearchService",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17FeedSearchServiceV"
  },
  "title" : "FeedSearchService"
}
-->

# FeedSearchService

A [`SearchService`](/documentation/PSReader/SearchService) for searching editions on PageSuite’s current system.

```
struct FeedSearchService
```

## Overview

`FeedSearchService` provides direct access to the PageSuite search API, allowing
you to search across articles and pages within those editions. Use this to
integrate PageSuite search into your own app-wide search system.

```swift
let service = FeedSearchService()

service.search(
    accountGuid: "ACCOUNT_GUID",
    query: "climate change",
    type: .editionArticle,
    publications: [(.app, "PUBLICATION_GUID_1"), (.app, "PUBLICATION_GUID_2")]
) { result in
    switch result {
    case .success(let response):
        for item in response.data ?? [] {
            print(item.headline ?? "")
        }
    case .failure(let error):
        print(error)
    }
}
```

To build a search screen on it, see [Building a Search Screen](/documentation/PSReader/Building-a-Search-Screen).

## Topics

### Creating a Search Service

[`init(session:)`](/documentation/PSReader/FeedSearchService/init(session:))

Creates a new feed search service.

### Searching

[`search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)`](/documentation/PSReader/FeedSearchService/search(accountGuid:query:type:publications:offset:limit:timeZone:completion:))

Searches for content across the specified publications.

[`search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)`](/documentation/PSReader/FeedSearchService/search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:))

Searches for content within a date range.

### Errors

[`FeedSearchService.SearchError`](/documentation/PSReader/FeedSearchService/SearchError)

Errors that can occur during a search request.

