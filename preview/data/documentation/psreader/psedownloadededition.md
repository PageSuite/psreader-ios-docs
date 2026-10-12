<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadedEdition",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20PSEDownloadedEditionV"
  },
  "title" : "PSEDownloadedEdition"
}
-->

# PSEDownloadedEdition

An edition source backed by a copy stored on device by
[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager).

```
struct PSEDownloadedEdition
```

## Overview

All page assets are read from the download cache, so the edition opens
and reads fully offline. Opening fails if the edition has not been
downloaded (or is still queued); check
[`isDownloaded(published:)`](/documentation/PSReader/PSEDownloadManager/isDownloaded(published:)) first, or use
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)), which falls back to
streaming automatically.

## Topics

### Opening a Downloaded Edition

[`open(published:)`](/documentation/PSReader/PSEDownloadedEdition/open(published:))

Opens the downloaded copy of an edition.

[`open(published:completion:)`](/documentation/PSReader/PSEDownloadedEdition/open(published:completion:))

Opens the downloaded copy of an edition.

### Content

[`published`](/documentation/PSReader/PSEDownloadedEdition/published)

The catalog entry this edition was opened from.

[`edition`](/documentation/PSReader/PSEDownloadedEdition/edition)

The edition content loaded from the stored copy: pages, spreads, and
sections.

