<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadObserver/downloadManager(_:downloadFor:didChangeState:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEDownloadObserverP15downloadManager_0D3For14didChangeStateyAA0bE0C_AA12PSEPublishedCAH08DownloadI0OtF"
  },
  "title" : "downloadManager(_:downloadFor:didChangeState:)"
}
-->

# downloadManager(_:downloadFor:didChangeState:)

Called whenever an edition’s download state changes, including
progress updates while downloading.

```
func downloadManager(_ downloadManager: PSEDownloadManager, downloadFor published: PSEPublished, didChangeState state: PSEDownloadManager.DownloadState)
```