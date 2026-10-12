<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadObserver",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEDownloadObserverP"
  },
  "title" : "PSEDownloadObserver"
}
-->

# PSEDownloadObserver

Receives download state changes from [`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager).

```
protocol PSEDownloadObserver : AnyObject
```

## Overview

Register with [`addObserver(_:published:)`](/documentation/PSReader/PSEDownloadManager/addObserver(_:published:)) to follow
one edition (a download button) or [`addObserver(_:)`](/documentation/PSReader/PSEDownloadManager/addObserver(_:))
to follow everything (a downloads screen). Called on the main thread.

## Topics

### Observing Downloads

[`downloadManager(_:downloadFor:didChangeState:)`](/documentation/PSReader/PSEDownloadObserver/downloadManager(_:downloadFor:didChangeState:))

Called whenever an edition’s download state changes, including
progress updates while downloading.

