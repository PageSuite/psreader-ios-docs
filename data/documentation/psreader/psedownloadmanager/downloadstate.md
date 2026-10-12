<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/DownloadState",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC13DownloadStateO"
  },
  "title" : "PSEDownloadManager.DownloadState"
}
-->

# PSEDownloadManager.DownloadState

The lifecycle state of an edition’s download.

```
enum DownloadState
```

## Overview

`errored` carries no underlying error; the failure is logged, and the
download can be retried by queuing again.

## Topics

### Before Downloading

[`PSEDownloadManager.DownloadState.notDownloaded`](/documentation/PSReader/PSEDownloadManager/DownloadState/notDownloaded)

No copy is stored and no download is queued or running.

[`PSEDownloadManager.DownloadState.queued`](/documentation/PSReader/PSEDownloadManager/DownloadState/queued)

Waiting in the download queue to start.

### Downloading

[`PSEDownloadManager.DownloadState.downloading(phase:phaseProgress:globalProgress:)`](/documentation/PSReader/PSEDownloadManager/DownloadState/downloading(phase:phaseProgress:globalProgress:))

Actively downloading. `phaseProgress` is 0…1 within the current
[`PSEDownloadManager.DownloadPhase`](/documentation/PSReader/PSEDownloadManager/DownloadPhase); `globalProgress` is 0…1 across the whole
download.

### After Downloading

[`PSEDownloadManager.DownloadState.downloaded`](/documentation/PSReader/PSEDownloadManager/DownloadState/downloaded)

A complete copy is stored on device and opens offline.

[`PSEDownloadManager.DownloadState.errored`](/documentation/PSReader/PSEDownloadManager/DownloadState/errored)

The download failed: the edition’s file list couldn’t be loaded,
or a file still failed after
[`maxDownloadRetryAttempts`](/documentation/PSReader/PSEDownloadManager/maxDownloadRetryAttempts) retries.

[`PSEDownloadManager.DownloadState.cancelled`](/documentation/PSReader/PSEDownloadManager/DownloadState/cancelled)

The download was canceled before it finished.

[`PSEDownloadManager.DownloadState.deleted`](/documentation/PSReader/PSEDownloadManager/DownloadState/deleted)

Not reported by [`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager): deleting a stored copy
reports [`PSEDownloadManager.DownloadState.notDownloaded`](/documentation/PSReader/PSEDownloadManager/DownloadState/notDownloaded) instead. Handle it as
[`PSEDownloadManager.DownloadState.notDownloaded`](/documentation/PSReader/PSEDownloadManager/DownloadState/notDownloaded).

