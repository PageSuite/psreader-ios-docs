<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/DownloadState/errored",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC13DownloadStateO7erroredyA2EmF"
  },
  "title" : "PSEDownloadManager.DownloadState.errored"
}
-->

# PSEDownloadManager.DownloadState.errored

The download failed: the edition’s file list couldn’t be loaded,
or a file still failed after
[`maxDownloadRetryAttempts`](/documentation/PSReader/PSEDownloadManager/maxDownloadRetryAttempts) retries.

```
case errored
```