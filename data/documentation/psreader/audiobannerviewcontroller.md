<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioBannerViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25AudioBannerViewControllerP"
  },
  "title" : "AudioBannerViewController"
}
-->

# AudioBannerViewController

A view controller used to present persistent audio controls as a banner.

```
@MainActor protocol AudioBannerViewController : UIViewController
```

## Overview

Instances are returned from [`audioBannerViewController()`](/documentation/PSReader/AudioDelegate/audioBannerViewController()) and are embedded
by the SDK either as a floating overlay or as part of the vertical layout stack depending
on [`isFloating`](/documentation/PSReader/AudioBannerViewController/isFloating).

Visibility is driven by the view’s own layout:

- Provide an intrinsic content height (via Auto Layout) to show the banner.
- Return zero height (or otherwise collapse the view) to hide the banner.

## Layout Behavior

- When `isFloating == true`, the banner floats above the reader content and is pinned to the
  bottom of the screen. The SDK automatically applies a bottom safe‑area inset equal to the
  banner’s height so content is not obscured.
- When `isFloating == false`, the banner is stacked below the reader; the reader’s height is
  reduced accordingly and no extra insets are applied.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate``

## Topics

### Positioning the Banner

[`isFloating`](/documentation/PSReader/AudioBannerViewController/isFloating)

Controls how the banner is positioned relative to the reader content.

