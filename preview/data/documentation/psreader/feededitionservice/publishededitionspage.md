<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/PublishedEditionsPage",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV21PublishedEditionsPageV"
  },
  "title" : "FeedEditionService.PublishedEditionsPage"
}
-->

# FeedEditionService.PublishedEditionsPage

One page of a date-range request.

```
struct PublishedEditionsPage
```

## Overview

Returned by
[`publishedEditions(publicationGUID:publicationName:startDate:endDate:pageNumber:pageSize:)`](/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:startDate:endDate:pageNumber:pageSize:)).
Each value is `nil` when the response leaves it out or sends it in
an unexpected shape, so one bad field never discards the rest.

## Topics

### Reading the Page

[`dates`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/dates)

The page’s publishing dates, newest first.

### Paging

[`pagination`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/pagination-swift.property)

Where this page sits in the whole range.

[`FeedEditionService.PublishedEditionsPage.Pagination`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/Pagination-swift.struct)

Paging details for a date-range request, counted in publishing
dates.

