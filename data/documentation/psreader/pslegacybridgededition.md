<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC"
  },
  "title" : "PSLegacyBridgedEdition"
}
-->

# PSLegacyBridgedEdition

An edition source that opens an edition saved with the legacy SDK in the
current reader.

```
final class PSLegacyBridgedEdition
```

## Overview

Records fabricated by [`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:))
and [`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)) are flagged
[`isBridged`](/documentation/PSReader/PSEPublished/isBridged); opening such an edition resolves the old
edition’s manifest and assets at open time. You normally never open one
directly — [`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) routes bridged
editions here automatically, with [`PSLegacyDefaultMigrationHooks`](/documentation/PSReader/PSLegacyDefaultMigrationHooks). Open
one yourself with [`open(published:hooks:onProgress:completion:)`](/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:completion:)) to
build its article pages with your own [`PSLegacyMigrationHooks`](/documentation/PSReader/PSLegacyMigrationHooks).

## Topics

### Opening a Migrated Download

[`open(published:hooks:onProgress:)`](/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:))

Opens a bridged legacy download.

[`open(published:hooks:onProgress:completion:)`](/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:completion:))

Opens a bridged legacy download.

[`PSLegacyBridgedEdition.OpenError`](/documentation/PSReader/PSLegacyBridgedEdition/OpenError)

Failures resolving the legacy download at open time.

### Content

[`published`](/documentation/PSReader/PSLegacyBridgedEdition/published)

The migrated catalog entry this edition was opened from.

[`edition`](/documentation/PSReader/PSLegacyBridgedEdition/edition)

The edition built from the legacy manifest at open time: the legacy
edition’s PDF pages in order, then one article page for each
[`PSLegacyMigratedArticle`](/documentation/PSReader/PSLegacyMigratedArticle) the hooks returned.

### Assets

[`resourceManager`](/documentation/PSReader/PSLegacyBridgedEdition/resourceManager)

This edition itself, which resolves resources against the edition’s
folder and falls back to the legacy backend for page files not stored
there yet.

[`pageSource`](/documentation/PSReader/PSLegacyBridgedEdition/pageSource)

This edition itself, which reports each spread’s state while it
prepares the spread’s page files, so the reader can show loading and
retry states.

[`pagePrefetching`](/documentation/PSReader/PSLegacyBridgedEdition/pagePrefetching)

This edition itself, which prepares the pages of the spreads near the
one the reader asks it to prefetch.

### Resolving Resources

[`resolveURL(resource:)`](/documentation/PSReader/PSLegacyBridgedEdition/resolveURL(resource:))

Returns a URL for the resource.

[`resolve(resource:)`](/documentation/PSReader/PSLegacyBridgedEdition/resolve(resource:))

Returns a location for the resource.

[`cachedData(for:)`](/documentation/PSReader/PSLegacyBridgedEdition/cachedData(for:))

Returns the resource’s bytes if it’s stored in the edition’s folder.

[`dataTask(for:completion:)`](/documentation/PSReader/PSLegacyBridgedEdition/dataTask(for:completion:))

Creates an HTTP fetch for the resource: an absolute `http` reference
as it is, or a page file from the legacy backend.

### Spread State

[`addObserver(_:forPageSpread:)`](/documentation/PSReader/PSLegacyBridgedEdition/addObserver(_:forPageSpread:))

Starts reporting a spread’s state to an observer, and starts preparing
the spread’s page files.

[`removeObserver(_:forPageSpread:)`](/documentation/PSReader/PSLegacyBridgedEdition/removeObserver(_:forPageSpread:))

Stops reporting a spread’s state to an observer.

[`retryDownload(for:)`](/documentation/PSReader/PSLegacyBridgedEdition/retryDownload(for:))

Retries the spread’s pages whose files failed to load.

### Prefetching

[`editionPrefetching(prefetchAtIndex:pagingMode:direction:)`](/documentation/PSReader/PSLegacyBridgedEdition/editionPrefetching(prefetchAtIndex:pagingMode:direction:))

Prepares the page files of the spreads near a spread.

