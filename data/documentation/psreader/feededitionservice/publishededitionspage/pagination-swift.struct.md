<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/PublishedEditionsPage/Pagination-swift.struct",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV21PublishedEditionsPageV10PaginationV"
  },
  "title" : "FeedEditionService.PublishedEditionsPage.Pagination"
}
-->

# FeedEditionService.PublishedEditionsPage.Pagination

Paging details for a date-range request, counted in publishing
dates.

```
struct Pagination
```

## Topics

### Position in the Range

[`page`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/Pagination-swift.struct/page)

This page’s number, starting from 1.

[`size`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/Pagination-swift.struct/size)

The page size the request asked for.

[`totalPages`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/Pagination-swift.struct/totalPages)

The number of pages in the whole range; at least 1.

[`total`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/Pagination-swift.struct/total)

The number of publishing dates in the whole range.

### Moving Between Pages

[`hasNext`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/Pagination-swift.struct/hasNext)

Whether a later page exists.

[`hasPrev`](/documentation/PSReader/FeedEditionService/PublishedEditionsPage/Pagination-swift.struct/hasPrev)

Whether an earlier page exists.

