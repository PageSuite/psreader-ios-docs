<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselConfiguration/hidesHeaderOnScroll",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21CarouselConfigurationV19hidesHeaderOnScrollSbvp"
  },
  "title" : "hidesHeaderOnScroll"
}
-->

# hidesHeaderOnScroll

Controls whether the carousel header (supplied via
[`init(globalConfig:carouselConfig:header:sections:)`](/documentation/PSReader/CarouselViewController/init(globalConfig:carouselConfig:header:sections:)))
hides as the content scrolls and reappears when scrolling back up or
changing page.

```
var hidesHeaderOnScroll: Bool
```

## Discussion

If set to `false` (default), the header remains fixed at the top.
Has no effect when no header is supplied.

> Note: Leave this `false` (or unset) when supplying a
> ``doc://com.pagesuite.PSReader/documentation/PSReader/DismissHeaderViewController`` so the close button stays reachable.