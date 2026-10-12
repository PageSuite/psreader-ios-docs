<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/MediaDelegate/pdfMediaOverlay(for:in:superview:)-2suug",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13MediaDelegatePAAE03pdfB7Overlay3for2in9superviewAA08PSEMediaE0CSgAA0I6ObjectC_AA7PSEPageCSo6UIViewCtF"
  },
  "title" : "pdfMediaOverlay(for:in:superview:)"
}
-->

# pdfMediaOverlay(for:in:superview:)

Returns `nil`, so the reader uses its built-in overlays:
`PSEMediaLinkOverlay` for link hotspots and
`PSEMediaArticleOverlay` for article hotspots.

```
@MainActor func pdfMediaOverlay(for mediaObject: PSEMediaObject, in page: PSEPage, superview: UIView) -> PSEMediaOverlay?
```

## Parameters

`mediaObject`

The media object embedded in the PDF page.

`page`

The PDF page containing the media object.

`superview`

The view in which the media overlay will be displayed.

## Return Value

`nil`.