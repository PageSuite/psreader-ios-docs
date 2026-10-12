<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/removeOutdatedDownload(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC22removeOutdatedDownload3foryAA12PSEPublishedC_tF"
  },
  "title" : "removeOutdatedDownload(for:)"
}
-->

# removeOutdatedDownload(for:)

Drops a downloaded edition whose content has since changed on the
server (a newer lastUpdatedTimestamp), so a fresh copy is fetched.

```
func removeOutdatedDownload(for published: PSEPublished)
```