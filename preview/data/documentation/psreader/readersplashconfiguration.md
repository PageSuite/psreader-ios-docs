<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderSplashConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25ReaderSplashConfigurationV"
  },
  "title" : "ReaderSplashConfiguration"
}
-->

# ReaderSplashConfiguration

Configuration object for customizing the splash screen displayed when opening
a published edition. The splash screen provides visual feedback during content
loading transitions, displaying the edition’s thumbnail, name, date, loading status.

```
struct ReaderSplashConfiguration
```

## Overview

Customize this configuration to align the splash screen’s appearance, including fonts,
colors, image layout, and error messaging, with your application’s overall branding
and user experience guidelines.

For the reader’s other options, see [Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/ReaderSplashConfiguration/init(globalConfig:))

Initializes a new splash screen configuration using defaults from the provided global SDK configuration.

### Edition Details

[`thumbnailContentMode`](/documentation/PSReader/ReaderSplashConfiguration/thumbnailContentMode)

Content mode determining how the edition thumbnail image is displayed within the splash screen.

[`editionNameLabel`](/documentation/PSReader/ReaderSplashConfiguration/editionNameLabel)

Configuration for the label displaying the edition name.

[`editionDateLabel`](/documentation/PSReader/ReaderSplashConfiguration/editionDateLabel)

Configuration for the label displaying the edition date or subtitle.

[`dateFormatter`](/documentation/PSReader/ReaderSplashConfiguration/dateFormatter)

Formatter used to generate display strings for the edition date shown on the splash screen.

### Progress

[`statusLabel`](/documentation/PSReader/ReaderSplashConfiguration/statusLabel)

Configuration for the label displaying the current loading status.

[`progressBarTintColor`](/documentation/PSReader/ReaderSplashConfiguration/progressBarTintColor)

Tint color of the progress bar indicating loading or download progress.

### Errors

[`errorTitleLabel`](/documentation/PSReader/ReaderSplashConfiguration/errorTitleLabel)

Configuration for the primary error title shown when content fails to load.

[`errorSubtitleLabel`](/documentation/PSReader/ReaderSplashConfiguration/errorSubtitleLabel)

Configuration for the secondary error subtitle providing additional details or instructions on loading errors.

[`errorRefreshIconTintColor`](/documentation/PSReader/ReaderSplashConfiguration/errorRefreshIconTintColor)

Tint color for the refresh icon displayed on the splash screen in case of loading errors.

### Appearance

[`liquidGlassPolicy`](/documentation/PSReader/ReaderSplashConfiguration/liquidGlassPolicy)

Liquid Glass policy for the reader splash screen.

