<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC19toggleDownloadState3forAC06ToggleE6StatusOAA12PSEPublishedC_tKF"
  },
  "title" : "toggleDownloadState(for:)"
}
-->

# toggleDownloadState(for:)

Advances an edition’s download the way a download button expects,
and returns which step it took as a [`PSEDownloadManager.ToggleDownloadStatus`](/documentation/PSReader/PSEDownloadManager/ToggleDownloadStatus): an
edition that isn’t downloaded is queued, a queued or running download
is canceled, and a downloaded edition’s copy is deleted.

```
@discardableResult func toggleDownloadState(for published: PSEPublished) throws -> ToggleDownloadStatus
```

## Discussion

Throws `PSDownloadError.noNetwork` or `.noWiFi` when queuing is not
currently allowed (offline, or the user restricted downloads to
Wi-Fi).