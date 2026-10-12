<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDownloadManager/downloadImmediately(published:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEDownloadManagerC19downloadImmediately9publishedyAA12PSEPublishedC_tF"
  },
  "title" : "downloadImmediately(published:)"
}
-->

# downloadImmediately(published:)

Starts an edition’s download at once, pushing any currently active
download back to the front of the queue. No effect if the edition is
already downloading or downloaded.

```
func downloadImmediately(published: PSEPublished)
```