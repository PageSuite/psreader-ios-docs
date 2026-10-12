<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/editionPrefetching(prefetchAtIndex:pagingMode:direction:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC18editionPrefetching15prefetchAtIndex10pagingMode9directionySi_AA015PSEditionPagingJ0OAA30PSEPageSpreadPrefetchDirectionOtF"
  },
  "title" : "editionPrefetching(prefetchAtIndex:pagingMode:direction:)"
}
-->

# editionPrefetching(prefetchAtIndex:pagingMode:direction:)

Moves the pages around a spread to the front of the download queue.

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

With a [`PSEPageSpreadPrefetchDirection.neutral`](/documentation/PSReader/PSEPageSpreadPrefetchDirection/neutral) direction the
edition prefetches the spread and the two spreads on each side of it;
otherwise it prefetches the spread and the next four in the reading
direction. Queued pages beyond the edition’s download limit are
canceled, so the latest request wins.