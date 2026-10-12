<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchService/search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)-4plkz",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13SearchServicePAAE6search11accountGuid5query4type12publications6offset5limit8timeZone10completionSo20NSURLSessionDataTaskCSgSS_SSAA0B4TypeOSayAA0b11PublicationR0OAG_SS2idtGS2i10Foundation04TimeM0Vys6ResultOyAA0B8ResponseVs5Error_pGctF"
  },
  "title" : "search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)"
}
-->

# search(accountGuid:query:type:publications:offset:limit:timeZone:completion:)

Searches for content across the specified publications, with default
pagination (`offset` `0`, `limit` `50`) and the current time zone.

```
@discardableResult func search(accountGuid: String, query: String, type: SearchType, publications: [(type: SearchPublicationType, id: String)], offset: Int = 0, limit: Int = 50, timeZone: TimeZone = .current, completion: @escaping (Result<SearchResponse, Error>) -> Void) -> URLSessionDataTask?
```