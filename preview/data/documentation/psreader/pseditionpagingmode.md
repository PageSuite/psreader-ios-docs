<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionPagingMode",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEditionPagingModeO"
  },
  "title" : "PSEditionPagingMode"
}
-->

# PSEditionPagingMode

How many pages the reader lays out per spread.

```
enum PSEditionPagingMode
```

## Overview

Chosen by [`PSEditionReaderViewController.LayoutDelegate`](/documentation/PSReader/PSEditionReaderViewController/LayoutDelegate-swift.protocol) (single-page
without one). [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) callbacks
and `scrollTo(index:)` speak in spread indices for the active mode.

## Topics

### Modes

[`PSEditionPagingMode.single`](/documentation/PSReader/PSEditionPagingMode/single)

One page per spread.

[`PSEditionPagingMode.double`](/documentation/PSReader/PSEditionPagingMode/double)

Two facing pages per spread, magazine-style.

