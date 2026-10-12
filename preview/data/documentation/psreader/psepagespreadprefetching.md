<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpreadPrefetching",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24PSEPageSpreadPrefetchingP"
  },
  "title" : "PSEPageSpreadPrefetching"
}
-->

# PSEPageSpreadPrefetching

Lets an edition source warm upcoming page assets as the user reads.

```
protocol PSEPageSpreadPrefetching
```

## Overview

The reader calls this as pages settle, passing the spread index the user
is likely to reach next. Sources that stream assets on demand (such as
[`PSEStreamingEdition`](/documentation/PSReader/PSEStreamingEdition)) use it to hide download latency; fully local
sources don’t need it.

## Topics

### Prefetching

[`editionPrefetching(prefetchAtIndex:pagingMode:direction:)`](/documentation/PSReader/PSEPageSpreadPrefetching/editionPrefetching(prefetchAtIndex:pagingMode:direction:))

Requests that assets for the spread at `index` be prepared.

