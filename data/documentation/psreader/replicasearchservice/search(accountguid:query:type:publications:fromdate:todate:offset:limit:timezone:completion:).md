<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReplicaSearchService/search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ReplicaSearchServiceC6search11accountGuid5query4type12publications8fromDate02toL06offset5limit8timeZone10completionSo20NSURLSessionDataTaskCSgSS_SSAA0C4TypeOSayAA0c11PublicationV0OAG_SS2idtG10Foundation0L0VSgA_S2iAX04TimeQ0Vys6ResultOyAA0C8ResponseVs5Error_pGctF"
  },
  "title" : "search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)"
}
-->

# search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)

Searches for pages within a date range.

```
@discardableResult func search(accountGuid: String, query: String, type: SearchType, publications: [(type: SearchPublicationType, id: String)], fromDate: Date?, toDate: Date?, offset: Int = 0, limit: Int = 50, timeZone: TimeZone = .current, completion: @escaping (Result<SearchResponse, Error>) -> Void) -> URLSessionDataTask?
```

## Parameters

`accountGuid`

The account GUID to search within.

`query`

The search query string.

`type`

The type of content to search for.

`publications`

An array of `(type, id)` tuples identifying the
publications to search across. The legacy endpoint searches only
the first.

`fromDate`

The inclusive start of the date range, or `nil`.

`toDate`

The inclusive end of the date range, or `nil`. The range is
applied only when BOTH dates are provided.

`offset`

The result offset for pagination.

`limit`

The maximum number of results to return.

`timeZone`

The time zone used to express the range as calendar days.

`completion`

A closure called with the search result.

## Return Value

The URL session task when one is directly available, or `nil`.

## Discussion

The legacy endpoint supports date-scoped search (`t=d` with `dfrom`/`dto`);
this is not part of the [`SearchService`](/documentation/PSReader/SearchService) protocol because the feed search
API has no server-side date filter. Pass `nil` for both dates to search
without a range.