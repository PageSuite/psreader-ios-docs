<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/editionPrefetching(prefetchAtIndex:pagingMode:direction:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC18editionPrefetching15prefetchAtIndex10pagingMode9directionySi_AA015PSEditionPagingK0OAA30PSEPageSpreadPrefetchDirectionOtF"
  },
  "title" : "editionPrefetching(prefetchAtIndex:pagingMode:direction:)"
}
-->

# editionPrefetching(prefetchAtIndex:pagingMode:direction:)

Prepares the page files of the spreads near a spread.

```
func editionPrefetching(prefetchAtIndex index: Int, pagingMode: PSEditionPagingMode, direction: PSEPageSpreadPrefetchDirection)
```

## Parameters

`index`

The spread index, in `pagingMode`’s spreads.

`pagingMode`

The paging mode the index refers to.

`direction`

The direction the user is reading in.

## Discussion

Reading forward, the edition prepares the next two spreads; reading
backward, the previous two; with a
[`PSEPageSpreadPrefetchDirection.neutral`](/documentation/PSReader/PSEPageSpreadPrefetchDirection/neutral) direction, the previous
spread and the next two.