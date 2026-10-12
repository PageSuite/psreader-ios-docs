<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpread/PageIterator",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13PSEPageSpreadO12PageIteratorV"
  },
  "title" : "PSEPageSpread.PageIterator"
}
-->

# PSEPageSpread.PageIterator

Iterates a spread’s non-nil pages in reading order.

```
struct PageIterator
```

## Overview

You rarely use it directly: `for page in spread` creates one for you.

## Topics

### Iterating

[`next()`](/documentation/PSReader/PSEPageSpread/PageIterator/next())

Returns the spread’s next non-nil page, or `nil` after the last
one.

