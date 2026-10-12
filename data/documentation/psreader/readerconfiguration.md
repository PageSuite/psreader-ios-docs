<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19ReaderConfigurationV"
  },
  "title" : "ReaderConfiguration"
}
-->

# ReaderConfiguration

Configuration object for customizing the prebuilt reader.

```
struct ReaderConfiguration
```

## Overview

Configure the appearance, behavior, and delegates required by the SDK’s primary
reader view. It provides fine-grained control over branding, typography, colors,
navigation elements, sharing, asset management, advertising, paywalls, and media playback.

Customize this configuration to ensure the reader integrates seamlessly with your
application’s branding, user experience, and overall design guidelines.

## Configuration Inheritance

`ReaderConfiguration` is created via [`init(globalConfig:)`](/documentation/PSReader/ReaderConfiguration/init(globalConfig:)) and inherits all
fonts, colors, and delegates from [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration). It is typically
accessed as a nested property of [`readerConfig`](/documentation/PSReader/ArchiveConfiguration/readerConfig), so
customizations flow through the archive config:

```swift
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.backgroundColor = .black
archiveConfig.readerConfig.navigationBar.itemSelectedBackgroundColor = .systemBlue
```

Sub-configurations ([`splashScreen`](/documentation/PSReader/ReaderConfiguration/splashScreen), [`navigationBar`](/documentation/PSReader/ReaderConfiguration/navigationBar), [`contentBrowser`](/documentation/PSReader/ReaderConfiguration/contentBrowser),
[`settings`](/documentation/PSReader/ReaderConfiguration/settings), [`legacyReader`](/documentation/PSReader/ReaderConfiguration/legacyReader)) inherit from the global config in the same way
and can be overridden individually.

To customize the reader screen, see [Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen).

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Theming>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/ReaderConfiguration/init(globalConfig:))

Initializes a new reader configuration, inheriting defaults from the provided global configuration.

### Appearance

[`primaryFont`](/documentation/PSReader/ReaderConfiguration/primaryFont)

The primary font applied to prominent text elements within the reader interface.

[`secondaryFont`](/documentation/PSReader/ReaderConfiguration/secondaryFont)

The secondary font used for supplementary text elements, subtitles,
labels, and other minor UI components.

[`brandColor`](/documentation/PSReader/ReaderConfiguration/brandColor)

The brand color used as an accent colors for highlights, selected elements, or progress indicators.

[`backgroundColor`](/documentation/PSReader/ReaderConfiguration/backgroundColor)

The overall background color of the reader interface.

[`liquidGlassPolicy`](/documentation/PSReader/ReaderConfiguration/liquidGlassPolicy)

Liquid Glass policy applied to the reader interface.

### Reader Screen

[`navigationBar`](/documentation/PSReader/ReaderConfiguration/navigationBar)

Configuration for the reader’s navigation bar, including fonts, colors, and item styling.

[`contentBrowser`](/documentation/PSReader/ReaderConfiguration/contentBrowser)

Configuration for the content browser used to navigate sections, pages, and articles within the reader.

[`splashScreen`](/documentation/PSReader/ReaderConfiguration/splashScreen)

Configuration for the splash screen displayed during content loading transitions.

### Settings Menu

[`settings`](/documentation/PSReader/ReaderConfiguration/settings)

Configuration for reader-specific user settings, such as text size adjustments, layout preferences, or reading mode options.

[`search`](/documentation/PSReader/ReaderConfiguration/search)

Optional search configuration enabling in-reader search.

### Delegates

[`assetDelegate`](/documentation/PSReader/ReaderConfiguration/assetDelegate)

Delegate responsible for providing custom UI assets (e.g., icons, images) for use within the reader.

[`shareDelegate`](/documentation/PSReader/ReaderConfiguration/shareDelegate)

Delegate providing sharing functionality.

[`audioDelegate`](/documentation/PSReader/ReaderConfiguration/audioDelegate)

Delegate providing audio functionality.

[`paywallDelegate`](/documentation/PSReader/ReaderConfiguration/paywallDelegate)

Optional delegate responsible for managing paywalls when accessing restricted or premium content.

[`advertDelegate`](/documentation/PSReader/ReaderConfiguration/advertDelegate)

Optional delegate controlling advertising integration within the reader interface.

[`mediaDelegate`](/documentation/PSReader/ReaderConfiguration/mediaDelegate)

Optional delegate enabling custom media functionality within the reader.

[`commentingDelegate`](/documentation/PSReader/ReaderConfiguration/commentingDelegate)

Optional delegate enabling commenting functionality within the reader.

[`navigationDelegate`](/documentation/PSReader/ReaderConfiguration/navigationDelegate)

Optional delegate handling navigation actions initiated from within the reader.

### Templated Content

[`baseURL`](/documentation/PSReader/ReaderConfiguration/baseURL)

The base URL used when rendering HTML.

### Replica Editions

[`useLegacyReplicaReader`](/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader)

When `true`, uses the legacy replica reader instead of the modern implementation.

[`legacyReader`](/documentation/PSReader/ReaderConfiguration/legacyReader)

Configuration settings specific to legacy replica reader interface.

