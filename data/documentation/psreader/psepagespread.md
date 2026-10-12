<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpread",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13PSEPageSpreadO"
  },
  "title" : "PSEPageSpread"
}
-->

# PSEPageSpread

One reader screenful: a single page, or two facing pages in double-page
mode.

```
enum PSEPageSpread
```

## Overview

Iterating a spread visits its non-nil pages in reading order.

For how the catalog and content models fit together, see
[The Edition Model](/documentation/PSReader/The-Edition-Model).

## Topics

### Spreads

[`PSEPageSpread.single(_:)`](/documentation/PSReader/PSEPageSpread/single(_:))

A lone page (single-page mode).

[`PSEPageSpread.double(left:right:)`](/documentation/PSReader/PSEPageSpread/double(left:right:))

Two facing pages; either side can be `nil` (a cover shown alone, or
an odd back page).

### Pages

[`referencePage()`](/documentation/PSReader/PSEPageSpread/referencePage())

The page that best represents the spread: editorial content is
preferred, so a spread pairing an advert with an editorial page
reports the editorial page. Advert-only spreads report the advert.

[`pages()`](/documentation/PSReader/PSEPageSpread/pages())

The spread’s non-nil pages, in reading order.

[`nonAdvertPages()`](/documentation/PSReader/PSEPageSpread/nonAdvertPages())

The spread’s pages excluding dedicated advert pages.

[`bookmarkablePages()`](/documentation/PSReader/PSEPageSpread/bookmarkablePages())

The spread’s pages whose [`bookmarkContext()`](/documentation/PSReader/PSEPage/bookmarkContext()) is
bookmarkable.

### Iterating

[`makeIterator()`](/documentation/PSReader/PSEPageSpread/makeIterator())

Returns an iterator over the spread’s non-nil pages in reading order:
the left page, then the right.

[`PSEPageSpread.PageIterator`](/documentation/PSReader/PSEPageSpread/PageIterator)

Iterates a spread’s non-nil pages in reading order.

