<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/Download",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC8DownloadV"
  },
  "title" : "PSEDownloadManager.Download"
}
-->

# PSEDownloadManager.Download

One entry in the manager’s download list: an edition and its state.

```
struct Download
```

## Topics

### Showing a List Row

[`published`](/documentation/PSReader/PSEDownloadManager/Download/published)

The edition being (or already) downloaded.

[`state`](/documentation/PSReader/PSEDownloadManager/Download/state)

The download’s current state.

[`date`](/documentation/PSReader/PSEDownloadManager/Download/date)

When the edition was last queued for download. For an edition
migrated from the legacy SDK, when that SDK downloaded it, or
when it migrated if that wasn’t recorded.

