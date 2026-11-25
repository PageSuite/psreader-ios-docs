<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/headerBackgroundColor",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC21headerBackgroundColorSo7UIColorCSgvp"
  },
  "title" : "headerBackgroundColor"
}
-->

# headerBackgroundColor

The header’s background color, for the backing the carousel paints above the
header while it shows: the status bar’s strip over a supplied header, or the
strip a navigation bar leaves above itself where the status bar isn’t at the
top, as in a side bar on iPhone Duo. Unset, a supplied header lends its view’s
background color, or the carousel’s own navigation bar its background color;
without either, the backing wears the section ribbon’s color.

```
@MainActor var headerBackgroundColor: UIColor? { get set }
```