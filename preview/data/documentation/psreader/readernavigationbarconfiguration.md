<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderNavigationBarConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader32ReaderNavigationBarConfigurationV"
  },
  "title" : "ReaderNavigationBarConfiguration"
}
-->

# ReaderNavigationBarConfiguration

Configuration object for customizing reader navigation bars.

```
struct ReaderNavigationBarConfiguration
```

## Overview

Use this configuration to adjust the colors, fonts, and styling of navigation items,
ensuring consistency with your application’s overall design language and branding.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Theming>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/ReaderNavigationBarConfiguration/init(globalConfig:))

Initializes a new navigation bar configuration with defaults derived from
the provided global SDK configuration.

### Buttons

[`itemLabelFont`](/documentation/PSReader/ReaderNavigationBarConfiguration/itemLabelFont)

The font used for navigation item labels within the reader navigation bar.

[`itemForegroundColor`](/documentation/PSReader/ReaderNavigationBarConfiguration/itemForegroundColor)

Foreground color (e.g., text or icons) of navigation items in their unselected state.

[`itemBackgroundColor`](/documentation/PSReader/ReaderNavigationBarConfiguration/itemBackgroundColor)

Background color of navigation items in their unselected state.

[`itemSelectedForegroundColor`](/documentation/PSReader/ReaderNavigationBarConfiguration/itemSelectedForegroundColor)

Foreground color (e.g., text or icons) of navigation items when selected.

[`itemSelectedBackgroundColor`](/documentation/PSReader/ReaderNavigationBarConfiguration/itemSelectedBackgroundColor)

Background color of navigation items when selected.

### Bar

[`dividerColor`](/documentation/PSReader/ReaderNavigationBarConfiguration/dividerColor)

Color of the divider line separating navigation bar items from other UI elements.

[`liquidGlassPolicy`](/documentation/PSReader/ReaderNavigationBarConfiguration/liquidGlassPolicy)

Liquid Glass policy for the reader navigation bar.

### Behavior

[`hidesBarsOnSwipe`](/documentation/PSReader/ReaderNavigationBarConfiguration/hidesBarsOnSwipe)

Hides the navigation bar and other views (such as comment buttons) when the user
scrolls down through content, and shows them again when scrolling back up.

