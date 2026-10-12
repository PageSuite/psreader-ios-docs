<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/retryDownload(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC13retryDownload3foryAA13PSEPageSpreadO_tF"
  },
  "title" : "retryDownload(for:)"
}
-->

# retryDownload(for:)

Retries the spread’s pages whose files failed to load.

```
func retryDownload(for pageSpread: PSEPageSpread)
```

## Parameters

`pageSpread`

The spread whose failed pages to retry.

## Discussion

Observers of the spread see its state change as the pages restart.