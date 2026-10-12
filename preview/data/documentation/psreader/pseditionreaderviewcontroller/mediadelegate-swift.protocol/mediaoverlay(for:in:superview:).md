<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/mediaOverlay(for:in:superview:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC13MediaDelegateP12mediaOverlay3for2in9superviewAA08PSEMediaI0CSgAA0M6ObjectC_AA7PSEPageCSo6UIViewCtF"
  },
  "title" : "mediaOverlay(for:in:superview:)"
}
-->

# mediaOverlay(for:in:superview:)

Returns the overlay view to place over a media hotspot, or `nil`
for no overlay. The default dispatches on `mediaObject.type` via
`defaultMediaOverlay(for:in:superview:)`.

```
func mediaOverlay(for mediaObject: PSEMediaObject, in page: PSEPage, superview: UIView) -> PSEMediaOverlay?
```