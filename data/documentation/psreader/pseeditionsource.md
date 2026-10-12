<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEditionSource",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16PSEEditionSourceP"
  },
  "title" : "PSEEditionSource"
}
-->

# PSEEditionSource

A reader-ready edition: the loaded content plus the machinery that
delivers its page assets.

```
protocol PSEEditionSource
```

## Overview

An edition source is what [`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:))
consumes. The SDK provides a source for every way an edition can be
backed:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEStreamingEdition`` — streams page assets on demand.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadedEdition`` — reads a copy stored by ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager``.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarksEdition`` — synthesizes an edition from saved bookmarks.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyBridgedEdition`` — presents a migrated legacy download.

You rarely construct these directly: [`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:))
picks the right one for an edition’s current state. Conform yourself only
to feed the reader content from a system the SDK does not know about;
`pagePrefetching`, `pageSource`, and `resourceManager` are defaulted, so a
minimal conformance supplies just `published` and `edition`.

To open an edition and show its progress, see [Opening an Edition](/documentation/PSReader/Opening-an-Edition).

## Topics

### Edition Content

[`published`](/documentation/PSReader/PSEEditionSource/published)

The catalog entry this source was opened from.

[`edition`](/documentation/PSReader/PSEEditionSource/edition)

The loaded edition content: pages, spreads, and sections.

### Asset Delivery

[`resourceManager`](/documentation/PSReader/PSEEditionSource/resourceManager)

Resolves the edition’s resource references to locations or data.
Defaults to a manager that reads the edition’s local cache and
fetches absolute URLs over HTTP.

[`pageSource`](/documentation/PSReader/PSEEditionSource/pageSource)

Reports per-spread asset availability for asynchronous sources.
Defaults to `nil` (all assets assumed available).

[`pagePrefetching`](/documentation/PSReader/PSEEditionSource/pagePrefetching)

Warms upcoming page assets while the user reads.
Defaults to `nil` (no prefetching).

