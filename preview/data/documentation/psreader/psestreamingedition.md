<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC"
  },
  "title" : "PSEStreamingEdition"
}
-->

# PSEStreamingEdition

An edition source that streams page assets from the network as the user
reads.

```
class PSEStreamingEdition
```

## Overview

Opening fetches only the edition manifest and the assets needed to show
the first pages (reported through `onProgress`); everything else downloads
on demand, driven by the reader’s prefetching. Fetched assets land in the
edition’s cache directory, so revisited pages don’t re-download. Requires
a network connection — for offline reading, queue the edition with
[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager) and open a [`PSEDownloadedEdition`](/documentation/PSReader/PSEDownloadedEdition) instead, or
let [`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) decide.

## Topics

### Opening an Edition

[`open(published:onProgress:)`](/documentation/PSReader/PSEStreamingEdition/open(published:onProgress:))

Opens an edition for streaming.

[`open(published:onProgress:completion:)`](/documentation/PSReader/PSEStreamingEdition/open(published:onProgress:completion:))

Opens an edition for streaming.

### Content

[`published`](/documentation/PSReader/PSEStreamingEdition/published)

The catalog entry this edition was opened from.

[`edition`](/documentation/PSReader/PSEStreamingEdition/edition)

The loaded edition content: pages, spreads, and sections.

### Assets

[`resourceManager`](/documentation/PSReader/PSEStreamingEdition/resourceManager)

This edition itself, which resolves resources against the edition’s
file list and downloads them on demand.

[`pageSource`](/documentation/PSReader/PSEStreamingEdition/pageSource)

This edition itself, which reports each spread’s download state so
the reader can show loading and retry states.

[`pagePrefetching`](/documentation/PSReader/PSEStreamingEdition/pagePrefetching)

This edition itself, which downloads the pages around the spreads
the reader asks it to prefetch.

### Resolving Resources

[`resolveURL(resource:)`](/documentation/PSReader/PSEStreamingEdition/resolveURL(resource:))

Returns a URL for the resource: the local file once it has
downloaded, otherwise its remote URL.

[`resolve(resource:)`](/documentation/PSReader/PSEStreamingEdition/resolve(resource:))

Returns the key the edition’s file list holds the resource under.

[`cachedData(for:)`](/documentation/PSReader/PSEStreamingEdition/cachedData(for:))

Returns the resource’s bytes if it has already downloaded.

[`dataTask(for:completion:)`](/documentation/PSReader/PSEStreamingEdition/dataTask(for:completion:))

Queues a download of an edition resource, ahead of the reader’s own
page downloads.

### Spread State

[`addObserver(_:forPageSpread:)`](/documentation/PSReader/PSEStreamingEdition/addObserver(_:forPageSpread:))

Starts reporting a spread’s download state to an observer.

[`removeObserver(_:forPageSpread:)`](/documentation/PSReader/PSEStreamingEdition/removeObserver(_:forPageSpread:))

Stops reporting a spread’s download state to an observer.

[`retryDownload(for:)`](/documentation/PSReader/PSEStreamingEdition/retryDownload(for:))

Retries the failed downloads for a spread’s pages.

### Prefetching

[`editionPrefetching(prefetchAtIndex:pagingMode:direction:)`](/documentation/PSReader/PSEStreamingEdition/editionPrefetching(prefetchAtIndex:pagingMode:direction:))

Moves the pages around a spread to the front of the download queue.

