<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReplicaSearchService/search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ReplicaSearchServiceC6search11accountGuid5query4type12publications6offset5limit8timeZone10completionSo20NSURLSessionDataTaskCSgSS_SSAA0C4TypeOSayAA0c11PublicationS0OAG_SS2idtGS2i10Foundation04TimeN0Vys6ResultOyAA0C8ResponseVs5Error_pGctF"
  },
  "title" : "search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)"
}
-->

# search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)

Searches for pages within the first of the specified publications.

```
@discardableResult func search(accountGuid: String, query: String, type: SearchType, publications: [(type: SearchPublicationType, id: String)], offset: Int, limit: Int, timeZone: TimeZone, completion: @escaping (Result<SearchResponse, Error>) -> Void) -> URLSessionDataTask?
```

## Parameters

`accountGuid`

Unused; the legacy endpoint is not account-scoped.

`query`

The search query string.

`type`

Unused; the legacy endpoint only returns page results.

`publications`

The publications to search. Only the first entry is
searched — the legacy endpoint does not support multi-publication
search.

`offset`

The result offset for pagination. Must be a multiple of
`limit`; the legacy endpoint paginates by page index.

`limit`

The maximum number of results to return.

`timeZone`

Unused.

`completion`

A closure called with the search result. Results are
mapped to [`SearchResult`](/documentation/PSReader/SearchResult) with [`type`](/documentation/PSReader/SearchResult/type) `"REPLICA_PAGE"`.

## Return Value

The URL session task when the publication’s latest edition is
already cached, otherwise `nil` while it is resolved asynchronously.