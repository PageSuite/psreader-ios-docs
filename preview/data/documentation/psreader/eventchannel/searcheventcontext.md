<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/SearchEventContext",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC06SearchB7ContextV"
  },
  "title" : "EventChannel.SearchEventContext"
}
-->

# EventChannel.SearchEventContext

Context object for search events.

```
struct SearchEventContext
```

## Topics

### Query

[`query`](/documentation/PSReader/EventChannel/SearchEventContext/query)

The search query string.

[`searchType`](/documentation/PSReader/EventChannel/SearchEventContext/searchType)

The search type filter applied to the query.

[`publications`](/documentation/PSReader/EventChannel/SearchEventContext/publications)

The publications that were searched. Contains all publications when
no filter is applied, or just the single filtered publication.

### Results

[`totalCount`](/documentation/PSReader/EventChannel/SearchEventContext/totalCount)

The total number of results returned by the search API.

