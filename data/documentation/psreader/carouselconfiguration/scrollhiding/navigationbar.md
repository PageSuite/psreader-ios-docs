<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselConfiguration/ScrollHiding/navigationBar",
  "metadataVersion" : "0.1.0",
  "role" : "Type Property",
  "symbol" : {
    "kind" : "Type Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21CarouselConfigurationV12ScrollHidingV13navigationBarAEvpZ"
  },
  "title" : "navigationBar"
}
-->

# navigationBar

The navigation bar above the carousel, on iOS 27 and later: it slides up with
the ribbons, which take its place, and a header that isn’t hiding moves up with
them. On earlier versions of iOS the bar stays in place.

```
static let navigationBar: CarouselConfiguration.ScrollHiding
```

## Discussion

Takes effect when the carousel sits in your own navigation controller, laid out
under its bar: set [`embedInNavigationController`](/documentation/PSReader/CarouselConfiguration/embedInNavigationController) to
`false` and include `.top` in [`ignoreSafeArea`](/documentation/PSReader/CarouselConfiguration/ignoreSafeArea).