<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedSearchService/search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17FeedSearchServiceV6search11accountGuid5query4type12publications8fromDate02toL06offset5limit8timeZone10completionSo20NSURLSessionDataTaskCSgSS_SSAA0C4TypeOSayAA0c11PublicationV0OAG_SS2idtG10Foundation0L0VSgA_S2iAX04TimeQ0Vys6ResultOyAA0C8ResponseVs5Error_pGctF"
  },
  "title" : "search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)"
}
-->

# search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)

Searches for content within a date range.

```
@discardableResult func search(accountGuid: String, query: String, type: SearchType, publications: [(type: SearchPublicationType, id: String)], fromDate: Date?, toDate: Date?, offset: Int = 0, limit: Int = 50, timeZone: TimeZone = .current, completion: @escaping (Result<SearchResponse, Error>) -> Void) -> URLSessionDataTask?
```

## Discussion

The search API accepts `fromDate`/`toDate` query parameters (calendar days,
interpreted in `timeZone`). This is not part of the [`SearchService`](/documentation/PSReader/SearchService) protocol;
pass `nil` for both dates to search without a range — the range is applied only
when BOTH dates are provided.