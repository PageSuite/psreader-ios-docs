<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEDownloadManager"
  },
  "title" : "PSEDownloadManager"
}
-->

# PSEDownloadManager

Downloads editions for offline reading and manages the stored copies.

```
class PSEDownloadManager
```

## Overview

Use the [`shared`](/documentation/PSReader/PSEDownloadManager/shared) singleton from the main thread. Queue an edition with
[`queueDownload(published:)`](/documentation/PSReader/PSEDownloadManager/queueDownload(published:)) (or [`toggleDownloadState(for:)`](/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:)) behind a
download button), observe progress through [`PSEDownloadObserver`](/documentation/PSReader/PSEDownloadObserver), and
open completed downloads via
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) — it prefers the
downloaded copy automatically.

Downloads run in two phases: [`PSEDownloadManager.DownloadPhase.splash`](/documentation/PSReader/PSEDownloadManager/DownloadPhase/splash) fetches the assets
needed to open the edition quickly, then [`PSEDownloadManager.DownloadPhase.main`](/documentation/PSReader/PSEDownloadManager/DownloadPhase/main) fetches
the rest. Apps migrating editions downloaded with the legacy SDK should
call [`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:)) once at startup.

To build a download button and a downloads list on it, see
[Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button).

## Topics

### Getting the Manager

[`shared`](/documentation/PSReader/PSEDownloadManager/shared)

The download manager. Use from the main thread.

### Starting Downloads

[`toggleDownloadState(for:)`](/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:))

Advances an edition’s download the way a download button expects,
and returns which step it took as a [`PSEDownloadManager.ToggleDownloadStatus`](/documentation/PSReader/PSEDownloadManager/ToggleDownloadStatus): an
edition that isn’t downloaded is queued, a queued or running download
is canceled, and a downloaded edition’s copy is deleted.

[`PSEDownloadManager.ToggleDownloadStatus`](/documentation/PSReader/PSEDownloadManager/ToggleDownloadStatus)

What [`toggleDownloadState(for:)`](/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:)) did.

[`queueDownload(published:)`](/documentation/PSReader/PSEDownloadManager/queueDownload(published:))

Adds an edition to the download queue (FIFO). No effect if it is
already queued, downloading, or downloaded.

[`downloadImmediately(published:)`](/documentation/PSReader/PSEDownloadManager/downloadImmediately(published:))

Starts an edition’s download at once, pushing any currently active
download back to the front of the queue. No effect if the edition is
already downloading or downloaded.

### Reading Download State

[`state(for:)`](/documentation/PSReader/PSEDownloadManager/state(for:))

The current download state for an edition, or `.notDownloaded` if it
has never been queued.

[`isDownloaded(published:)`](/documentation/PSReader/PSEDownloadManager/isDownloaded(published:))

Whether a completed download exists for the edition.

[`downloadedEdition(for:)`](/documentation/PSReader/PSEDownloadManager/downloadedEdition(for:))

The stored catalog entry of the edition’s completed download, or
`nil` if none exists.

[`downloads`](/documentation/PSReader/PSEDownloadManager/downloads)

Every known download, newest activity last. Drive a downloads screen
from this (the manager is an `ObservableObject`).

[`PSEDownloadManager.Download`](/documentation/PSReader/PSEDownloadManager/Download)

One entry in the manager’s download list: an edition and its state.

[`PSEDownloadManager.DownloadState`](/documentation/PSReader/PSEDownloadManager/DownloadState)

The lifecycle state of an edition’s download.

[`PSEDownloadManager.DownloadPhase`](/documentation/PSReader/PSEDownloadManager/DownloadPhase)

The stage a download is in.

### Observing Downloads

[`addObserver(_:published:)`](/documentation/PSReader/PSEDownloadManager/addObserver(_:published:))

Starts observing one edition’s download and returns its current
state (so UI can render immediately without a race). Observers are
held weakly.

[`addObserver(_:)`](/documentation/PSReader/PSEDownloadManager/addObserver(_:))

Starts observing every edition’s download state. Observers are held
weakly.

[`removeObserver(_:)`](/documentation/PSReader/PSEDownloadManager/removeObserver(_:))

Stops delivering state changes to the observer.

### Canceling and Deleting

[`cancelDownload(for:)`](/documentation/PSReader/PSEDownloadManager/cancelDownload(for:))

Cancels an in-progress or queued download for an edition. No effect if
the edition is not currently downloading.

[`cancelAllDownloads()`](/documentation/PSReader/PSEDownloadManager/cancelAllDownloads())

Cancels every in-progress and queued download.

[`removeDownload(for:)`](/documentation/PSReader/PSEDownloadManager/removeDownload(for:))

Deletes a downloaded edition from disk. No effect unless the edition is
fully downloaded.

[`deleteDownloads()`](/documentation/PSReader/PSEDownloadManager/deleteDownloads())

Deletes every downloaded edition from disk.

[`removeOutdatedDownload(for:)`](/documentation/PSReader/PSEDownloadManager/removeOutdatedDownload(for:))

Drops a downloaded edition whose content has since changed on the
server (a newer lastUpdatedTimestamp), so a fresh copy is fetched.

### Tuning Downloads

[`concurrentFileDownloads`](/documentation/PSReader/PSEDownloadManager/concurrentFileDownloads)

How many files one edition download fetches concurrently.

[`maxDownloadRetryAttempts`](/documentation/PSReader/PSEDownloadManager/maxDownloadRetryAttempts)

How many times a failed file fetch is retried before the download
errors.

### Migrating From the Legacy SDK

[`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:))

Adds the editions downloaded with the legacy SDK to [`downloads`](/documentation/PSReader/PSEDownloadManager/downloads).

