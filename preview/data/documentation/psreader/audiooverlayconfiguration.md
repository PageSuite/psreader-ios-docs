<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioOverlayConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25AudioOverlayConfigurationV"
  },
  "title" : "AudioOverlayConfiguration"
}
-->

# AudioOverlayConfiguration

Configuration structure for customizing the appearance of audio overlays.

```
struct AudioOverlayConfiguration
```

## Overview

This structure defines the visual styling and behavior of the default audio overlay interface.
Use this configuration to customize colors, fonts, and other visual elements to match your
application’s design system.

```swift
var config = AudioOverlayConfiguration(globalConfig: globalConfig)
config.brandColor = .systemPurple
config.titleLabel = LabelConfiguration(
    font: UIFont(name: "Georgia", size: 12)!,
    pointSize: 20,
    color: .label
)
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechProvider``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlay``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/AudioOverlayConfiguration/init(globalConfig:))

Creates a new audio overlay configuration using global SDK settings.

### Colors

[`brandColor`](/documentation/PSReader/AudioOverlayConfiguration/brandColor)

The primary brand color used for interactive elements and accent colors.

[`backgroundColor`](/documentation/PSReader/AudioOverlayConfiguration/backgroundColor)

The background color of the audio overlay interface.

[`liquidGlassPolicy`](/documentation/PSReader/AudioOverlayConfiguration/liquidGlassPolicy)

Liquid Glass policy for the audio overlay.

### Labels

[`titleLabel`](/documentation/PSReader/AudioOverlayConfiguration/titleLabel)

Configuration for the main title label displaying article or content titles.

[`subtitleLabel`](/documentation/PSReader/AudioOverlayConfiguration/subtitleLabel)

Configuration for the subtitle label displaying additional content information.

[`elapsedLabel`](/documentation/PSReader/AudioOverlayConfiguration/elapsedLabel)

Configuration for the elapsed time label showing playback progress.

[`remainingLabel`](/documentation/PSReader/AudioOverlayConfiguration/remainingLabel)

Configuration for the remaining time label showing time left in playback.

### Icons

[`assetDelegate`](/documentation/PSReader/AudioOverlayConfiguration/assetDelegate)

Asset delegate for loading custom icons and imagery within the audio interface.

