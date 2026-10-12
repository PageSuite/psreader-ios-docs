<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/didZoom(toScale:pageIndex:pagingMode:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14ScrollDelegateP7didZoom7toScale9pageIndex10pagingModey14CoreFoundation7CGFloatV_SiAA0b6PagingO0OtF"
  },
  "title" : "didZoom(toScale:pageIndex:pagingMode:)"
}
-->

# didZoom(toScale:pageIndex:pagingMode:)

Called when a zoom gesture on a PDF page ends (not continuously
during the pinch). Optional — defaults to a no-op.

```
func didZoom(toScale scale: CGFloat, pageIndex: Int, pagingMode: PSEditionPagingMode)
```