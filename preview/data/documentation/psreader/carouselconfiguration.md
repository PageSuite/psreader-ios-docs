<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21CarouselConfigurationV"
  },
  "title" : "CarouselConfiguration"
}
-->

# CarouselConfiguration

Configuration object for customizing the prebuilt carousel interface.

```
struct CarouselConfiguration
```

## Overview

The carousel is the primary user interface component for presenting various
types of content, including editions on PageSuite’s current system, legacy
replica editions, bookmarks, and downloads. It incorporates horizontal navigation through
sections and optional subsections.

Customize this configuration to control appearance, navigation, layout behaviors,
and integration with paywalls or navigation controllers.

```swift
var carouselConfig = CarouselConfiguration(globalConfig: globalConfig)
carouselConfig.embedInNavigationController = false
carouselConfig.hidesHeaderOnScroll = true

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    carouselConfig: carouselConfig,
    header: headerViewController,
    sections: sections
)
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/CarouselConfiguration/init(globalConfig:))

Initializes a new carousel configuration using the provided global configuration.

### Appearance

[`backgroundColor`](/documentation/PSReader/CarouselConfiguration/backgroundColor)

Background color displayed behind the entire carousel interface.

### Ribbons

[`sectionRibbon`](/documentation/PSReader/CarouselConfiguration/sectionRibbon)

Configuration for the primary section ribbon displayed horizontally at the top of the carousel.

[`subsectionRibbon`](/documentation/PSReader/CarouselConfiguration/subsectionRibbon)

Configuration for the optional subsection ribbon displayed beneath the section ribbon.

### Header

[`hidesHeaderOnScroll`](/documentation/PSReader/CarouselConfiguration/hidesHeaderOnScroll)

Controls whether the carousel header (supplied via
[`init(globalConfig:carouselConfig:header:sections:)`](/documentation/PSReader/CarouselViewController/init(globalConfig:carouselConfig:header:sections:)))
hides as the content scrolls and reappears when scrolling back up or
changing page.

### Fitting Into Your Layout

[`embedInNavigationController`](/documentation/PSReader/CarouselConfiguration/embedInNavigationController)

Indicates whether the carousel should automatically embed itself
within a navigation controller. If you are not using publication kiosks,
it is recommended to disable this feature.

[`ignoreSafeArea`](/documentation/PSReader/CarouselConfiguration/ignoreSafeArea)

Defines which safe-area edges should be ignored by the carousel interface.

### Paywalls

[`paywallDelegate`](/documentation/PSReader/CarouselConfiguration/paywallDelegate)

Optional delegate responsible for handling paywall interactions for content
accessed via the carousel. If set, the SDK uses this delegate to present paywalls
when accessing premium or protected content.

