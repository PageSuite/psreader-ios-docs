<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/defaultMediaOverlay(for:in:superview:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC13MediaDelegatePAAE07defaultF7Overlay3for2in9superviewAA08PSEMediaI0CSgAA0M6ObjectC_AA7PSEPageCSo6UIViewCtF"
  },
  "title" : "defaultMediaOverlay(for:in:superview:)"
}
-->

# defaultMediaOverlay(for:in:superview:)

Returns the reader’s standard overlay for a hotspot.

```
func defaultMediaOverlay(for mediaObject: PSEMediaObject, in page: PSEPage, superview: UIView) -> PSEMediaOverlay?
```

## Parameters

`mediaObject`

The hotspot to cover.

`page`

The page hosting the hotspot.

`superview`

The page view the reader adds the overlay to, passed
through to the overlay’s initializer.

## Return Value

The standard overlay, or `nil` when the hotspot’s type has
none.

## Discussion

Call this from your own [`mediaOverlay(for:in:superview:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/mediaOverlay(for:in:superview:)) to keep the
standard behavior for the hotspots you don’t customize. The hotspot’s
`type` is matched case-insensitively: `link` gets a
[`PSEMediaLinkOverlay`](/documentation/PSReader/PSEMediaLinkOverlay), `article` gets a [`PSEMediaArticleOverlay`](/documentation/PSReader/PSEMediaArticleOverlay),
and any other type gets no overlay.