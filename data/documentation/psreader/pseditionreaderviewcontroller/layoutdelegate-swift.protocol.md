<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/LayoutDelegate-swift.protocol",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14LayoutDelegateP"
  },
  "title" : "PSEditionReaderViewController.LayoutDelegate"
}
-->

# PSEditionReaderViewController.LayoutDelegate

Decides between single-page and double-page presentation.

```
protocol LayoutDelegate : AnyObject
```

## Overview

Without a delegate the reader always uses single-page mode. A typical
implementation returns [`PSEditionPagingMode.double`](/documentation/PSReader/PSEditionPagingMode/double) for regular
horizontal size classes in landscape.

## Topics

### Choosing a Paging Mode

[`pagingMode(forTraits:size:)`](/documentation/PSReader/PSEditionReaderViewController/LayoutDelegate-swift.protocol/pagingMode(forTraits:size:))

The paging mode to use for the given traits and size. Called on
layout changes (rotation, window resize).

