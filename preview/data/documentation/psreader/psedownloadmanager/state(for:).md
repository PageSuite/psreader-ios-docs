<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/state(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC5state3forAC13DownloadStateOAA12PSEPublishedC_tF"
  },
  "title" : "state(for:)"
}
-->

# state(for:)

The current download state for an edition, or `.notDownloaded` if it
has never been queued.

```
func state(for published: PSEPublished) -> DownloadState
```