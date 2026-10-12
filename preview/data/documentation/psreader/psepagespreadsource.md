<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpreadSource",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEPageSpreadSourceP"
  },
  "title" : "PSEPageSpreadSource"
}
-->

# PSEPageSpreadSource

Exposes per-spread asset availability for editions whose pages arrive
asynchronously.

```
protocol PSEPageSpreadSource : AnyObject
```

## Overview

The reader observes the spreads it displays so it can show loading and
retry states. Sources with all assets locally available leave
`PSEEditionSource.pageSource` as `nil` instead of conforming.

## Topics

### Observing Spread State

[`addObserver(_:forPageSpread:)`](/documentation/PSReader/PSEPageSpreadSource/addObserver(_:forPageSpread:))

Starts delivering state updates for a spread to the observer.

[`removeObserver(_:forPageSpread:)`](/documentation/PSReader/PSEPageSpreadSource/removeObserver(_:forPageSpread:))

Stops delivering state updates for a spread to the observer.

### Recovering From Failures

[`retryDownload(for:)`](/documentation/PSReader/PSEPageSpreadSource/retryDownload(for:))

Retries a failed asset download for a spread.

