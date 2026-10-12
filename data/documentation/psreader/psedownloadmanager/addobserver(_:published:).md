<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/addObserver(_:published:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC11addObserver_9publishedAC13DownloadStateOAA0bE0_p_AA12PSEPublishedCtF"
  },
  "title" : "addObserver(_:published:)"
}
-->

# addObserver(_:published:)

Starts observing one edition’s download and returns its current
state (so UI can render immediately without a race). Observers are
held weakly.

```
@discardableResult func addObserver(_ observer: PSEDownloadObserver, published: PSEPublished) -> DownloadState
```

## Parameters

`observer`

The observer to notify of the edition’s state changes.

`published`

The edition to observe.

## Return Value

The edition’s current download state, or
[`PSEDownloadManager.DownloadState.notDownloaded`](/documentation/PSReader/PSEDownloadManager/DownloadState/notDownloaded) if it has never been queued.