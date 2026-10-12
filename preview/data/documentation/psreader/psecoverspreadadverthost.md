<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSECoverSpreadAdvertHost",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24PSECoverSpreadAdvertHostP"
  },
  "title" : "PSECoverSpreadAdvertHost"
}
-->

# PSECoverSpreadAdvertHost

Marks the reader’s container for an advert that shares the cover’s spread
(the page-zero position beside the cover in double-page mode).

```
protocol PSECoverSpreadAdvertHost : AnyObject
```

## Overview

An advert view controller can check whether its parent adopts this
protocol, once embedded, to tell the cover slot from a full page:

```swift
override func didMove(toParent parent: UIViewController?) {
    super.didMove(toParent: parent)
    isBesideCover = parent is PSECoverSpreadAdvertHost
}
```