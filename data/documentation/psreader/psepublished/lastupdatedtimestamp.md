<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/lastUpdatedTimestamp",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished(py)lastUpdatedTimestamp"
  },
  "title" : "lastUpdatedTimestamp"
}
-->

# lastUpdatedTimestamp

A Unix timestamp of the edition’s last update, as sent by the
backend.

```
@objc var lastUpdatedTimestamp: Int
```

## Discussion

[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager) compares it with a downloaded copy’s value to
spot content that changed after the download.