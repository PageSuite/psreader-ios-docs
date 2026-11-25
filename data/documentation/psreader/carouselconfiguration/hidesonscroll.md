<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselConfiguration/hidesOnScroll",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21CarouselConfigurationV13hidesOnScrollAC0F6HidingVvp"
  },
  "title" : "hidesOnScroll"
}
-->

# hidesOnScroll

The parts of the carousel’s chrome that hide as the content scrolls down, and
reappear when it scrolls back up or changes page. See [`CarouselConfiguration.ScrollHiding`](/documentation/PSReader/CarouselConfiguration/ScrollHiding).

```
var hidesOnScroll: ScrollHiding
```

## Discussion

Empty by default: the chrome stays fixed at the top.

> Note: Leave out ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselConfiguration/ScrollHiding/header`` when supplying a
> ``doc://com.pagesuite.PSReader/documentation/PSReader/DismissHeaderViewController`` so the close button stays reachable.