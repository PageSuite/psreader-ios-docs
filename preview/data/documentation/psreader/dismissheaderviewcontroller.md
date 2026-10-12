<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DismissHeaderViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)DismissHeaderViewController"
  },
  "title" : "DismissHeaderViewController"
}
-->

# DismissHeaderViewController

A prebuilt carousel header containing a single dismiss (close) button.

```
@MainActor final class DismissHeaderViewController
```

## Overview

Pass an instance as the `header` of a [`CarouselViewController`](/documentation/PSReader/CarouselViewController) to add an
out-of-the-box close button, typically when the carousel is presented modally.

```swift
let carousel = CarouselViewController(
    globalConfig: globalConfig,
    carouselConfig: carouselConfig,
    header: DismissHeaderViewController(),
    sections: sections
)
present(carousel, animated: true)
```

By default, tapping the button calls `dismiss(animated:)`. Because the header
is installed as a child of the presented carousel, UIKit forwards the request
up to the carousel’s presenter and tears the carousel down — no extra wiring
required. Supply `onClose` to perform custom behavior instead (for example
when the carousel is embedded rather than presented).

> Note: A dismiss button should remain reachable, so leave
> ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselConfiguration/hidesHeaderOnScroll`` set to `false` (the
> default) when using this header.

For the carousel’s other options, see [Setting Up the Carousel](/documentation/PSReader/Setting-Up-the-Carousel).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ButtonConfiguration``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController``

## Topics

### Creating a Dismiss Header

[`init(config:onClose:)`](/documentation/PSReader/DismissHeaderViewController/init(config:onClose:))

Creates a dismiss header.

