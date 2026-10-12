<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselConfiguration/embedInNavigationController",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21CarouselConfigurationV27embedInNavigationControllerSbvp"
  },
  "title" : "embedInNavigationController"
}
-->

# embedInNavigationController

Indicates whether the carousel should automatically embed itself
within a navigation controller. If you are not using publication kiosks,
it is recommended to disable this feature.

```
var embedInNavigationController: Bool
```

## Discussion

If set to `true` (default), the carousel manages its own navigation controller.
Set to `false` if embedding manually.

> Tip: Set this to `false` when you embed the ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController`` inside
> your own `UINavigationController`.