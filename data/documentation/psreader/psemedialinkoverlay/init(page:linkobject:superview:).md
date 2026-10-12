<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaLinkOverlay/init(page:linkObject:superview:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEMediaLinkOverlayC4page10linkObject9superviewAcA7PSEPageC_AA0bG0CSo6UIViewCtcfc"
  },
  "title" : "init(page:linkObject:superview:)"
}
-->

# init(page:linkObject:superview:)

Creates a link overlay that responds to taps.

```
@MainActor init(page: PSEPage, linkObject: PSEMediaObject, superview: UIView)
```

## Parameters

`page`

The page hosting the hotspot.

`linkObject`

The `link` hotspot to cover. Its `target` is the link
a tap follows.

`superview`

The page view the overlay sits in. The overlay’s tap
waits for that view’s double-tap recognizers to fail, so
double-tap zooming keeps working over the hotspot.