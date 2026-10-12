<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchService/search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13SearchServiceP6search11accountGuid5query4type12publications6offset5limit8timeZone10completionSo20NSURLSessionDataTaskCSgSS_SSAA0B4TypeOSayAA0b11PublicationR0OAG_SS2idtGS2i10Foundation04TimeM0Vys6ResultOyAA0B8ResponseVs5Error_pGctF"
  },
  "title" : "search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)"
}
-->

# search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)

Searches for content across the specified publications.

```
@discardableResult func search(accountGuid: String, query: String, type: SearchType, publications: [(type: SearchPublicationType, id: String)], offset: Int, limit: Int, timeZone: TimeZone, completion: @escaping (Result<SearchResponse, Error>) -> Void) -> URLSessionDataTask?
```

## Parameters

`accountGuid`

The account GUID to search within.

`query`

The search query string.

`type`

The type of content to search for.

`publications`

An array of `(type, id)` tuples identifying the publications to
search across.

`offset`

The result offset for pagination.

`limit`

The maximum number of results to return.

`timeZone`

The time zone for date-sensitive filtering.

`completion`

A closure called with the search result.

## Return Value

The URL session task when one is directly available, or `nil`.