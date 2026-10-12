<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaArticleOverlay/init(page:articleObject:superview:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSEMediaArticleOverlayC4page13articleObject9superviewAcA7PSEPageC_AA0bG0CSo6UIViewCtcfc"
  },
  "title" : "init(page:articleObject:superview:)"
}
-->

# init(page:articleObject:superview:)

Creates an article overlay that responds to taps.

```
@MainActor init(page: PSEPage, articleObject: PSEMediaObject, superview: UIView)
```

## Parameters

`page`

The page hosting the hotspot.

`articleObject`

The `article` hotspot to cover. Its `feedPageGUID`
names the page a tap jumps to.

`superview`

The page view the overlay sits in. The overlay’s tap
waits for that view’s double-tap recognizers to fail, so
double-tap zooming keeps working over the hotspot.