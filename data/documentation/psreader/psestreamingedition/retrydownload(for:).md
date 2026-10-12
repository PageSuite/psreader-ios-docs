<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/retryDownload(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC13retryDownload3foryAA13PSEPageSpreadO_tF"
  },
  "title" : "retryDownload(for:)"
}
-->

# retryDownload(for:)

Retries the failed downloads for a spread’s pages.

```
func retryDownload(for pageSpread: PSEPageSpread)
```

## Parameters

`pageSpread`

The spread whose failed downloads to retry.

## Discussion

Observers of the spread see its state change as the downloads
restart.