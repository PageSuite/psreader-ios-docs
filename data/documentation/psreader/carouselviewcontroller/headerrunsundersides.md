<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/headerRunsUnderSides",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC20headerRunsUnderSidesSbvp"
  },
  "title" : "headerRunsUnderSides"
}
-->

# headerRunsUnderSides

Whether a supplied header runs under the sides the carousel runs under
([`ignoreSafeArea`](/documentation/PSReader/CarouselConfiguration/ignoreSafeArea)), as for a side bar on iPhone Duo. On
by default, as the ribbons do: the header’s view takes those sides as its safe
area, so a header laid out against its safe area layout guide keeps its controls
clear while its background reaches the edge. Off, the header keeps inside the
horizontal safe area however it lays itself out, and the carousel paints
[`headerBackgroundColor`](/documentation/PSReader/CarouselViewController/headerBackgroundColor) beside it. Set before the carousel shows.

```
@MainActor var headerRunsUnderSides: Bool
```