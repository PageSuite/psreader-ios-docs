<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18FeedEditionServiceV17publishedEditions15publicationGUID0G4Name0E6Domain9usesCacheSayAA16PSEPublishedDateCGSS_SSSgALSbtYaKF"
  },
  "title" : "publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:)"
}
-->

# publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:)

Returns the published-edition catalog for a publication, grouped
by date (newest first).

```
func publishedEditions(publicationGUID: String, publicationName: String? = nil, publishedDomain: String? = nil, usesCache: Bool = true) async throws -> [PSEPublishedDate]
```

## Parameters

`publicationGUID`

The publication GUID.

`publicationName`

A display name to copy onto each returned
edition, or `nil` to leave it empty.

`publishedDomain`

The base domain the catalog is hosted on, or
`nil` for the default domain. Pass a value only if your
publication’s content is hosted elsewhere.

`usesCache`

Whether a stored copy of this exact request may be
returned without a network request. Each request is unique to
the second, so this rarely has an effect. Falling back to the
last stored catalog when the request fails applies either way.

## Return Value

The publication’s catalog, one [`PSEPublishedDate`](/documentation/PSReader/PSEPublishedDate) per
publishing date.

## Discussion

The service requests a fresh catalog each time. When the request
fails, for example offline, it returns the last catalog it stored
for the publication instead.

> Throws: ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionServiceError/invalidResponse`` when there’s no
> catalog to return: the request failed with no stored copy to fall
> back to, or the backend sent something other than a catalog. A
> response that isn’t JSON at all throws the decoding error.