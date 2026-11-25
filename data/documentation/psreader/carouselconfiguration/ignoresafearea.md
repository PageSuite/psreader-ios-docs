<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselConfiguration/ignoreSafeArea",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21CarouselConfigurationV14ignoreSafeAreaSo10UIRectEdgeVvp"
  },
  "title" : "ignoreSafeArea"
}
-->

# ignoreSafeArea

Defines which safe-area edges should be ignored by the carousel interface.

```
var ignoreSafeArea: UIRectEdge
```

## Discussion

Customize this property to control content extension beyond safe-area boundaries.

`.left` and `.right` by default: the carousel spans the width where the system
insets its sides, as for a side bar on iPhone Duo or a notch in landscape. Its
ribbons run under the side bar with their titles kept clear of it, and so does a
header supplied to it, whose view takes those sides as its safe area: lay the
header out against its safe area layout guide and its controls keep clear while
its background reaches the edge. The pages keep inside the horizontal safe area,
and above the header the carousel paints the header view’s background color, or
[`headerBackgroundColor`](/documentation/PSReader/CarouselViewController/headerBackgroundColor). Leave the sides out to keep the
whole carousel inside the horizontal safe area instead.