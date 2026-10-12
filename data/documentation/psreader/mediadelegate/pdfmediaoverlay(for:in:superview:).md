<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/MediaDelegate/pdfMediaOverlay(for:in:superview:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13MediaDelegateP03pdfB7Overlay3for2in9superviewAA08PSEMediaE0CSgAA0I6ObjectC_AA7PSEPageCSo6UIViewCtF"
  },
  "title" : "pdfMediaOverlay(for:in:superview:)"
}
-->

# pdfMediaOverlay(for:in:superview:)

Provides a custom media overlay for an embedded media object within a PDF page.

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

A media overlay to display, or `nil` to keep the reader’s standard overlay for the media object.

## Discussion

Implement this method to present custom media experiences (such as video or
interactive content) for media objects embedded in an edition’s classic PDF pages.