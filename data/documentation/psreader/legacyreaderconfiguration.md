<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/LegacyReaderConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25LegacyReaderConfigurationV"
  },
  "title" : "LegacyReaderConfiguration"
}
-->

# LegacyReaderConfiguration

Configuration object for customizing the appearance, behavior, and sharing
strategies of the legacy replica reader.

```
struct LegacyReaderConfiguration
```

## Overview

The legacy replica reader is a traditional PDF-based reading interface retained
for backward compatibility. This reader uses a distinct set of navigation controls
and sharing functionality compared to the newer reader.

Sharing customization within the legacy reader is performed through template strings
containing placeholders (e.g., `{{{HEADLINE}}}`). These placeholders are dynamically
replaced by the SDK at runtime.

Customize this configuration to adjust navigation options, sharing templates,
and basic UI settings for the legacy reader interface.

For the reader’s other options, see [Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/LegacyReaderConfiguration/init(globalConfig:))

Initializes a new legacy reader configuration using defaults inherited from the global SDK configuration.

### Navigation Bars

[`navigationBarItems`](/documentation/PSReader/LegacyReaderConfiguration/navigationBarItems)

Navigation items enabled for the main reading interface of the legacy reader.

[`articleNavigationBarItems`](/documentation/PSReader/LegacyReaderConfiguration/articleNavigationBarItems)

Navigation items enabled when viewing articles within the legacy reader.

[`LegacyReaderConfiguration.NavigationBarItem`](/documentation/PSReader/LegacyReaderConfiguration/NavigationBarItem)

An option set representing available navigation bar items within the legacy reader.

[`navigationBarShadows`](/documentation/PSReader/LegacyReaderConfiguration/navigationBarShadows)

Enables or disables shadows beneath navigation bars in the legacy reader interface.

### Sharing

[`shareTemplater`](/documentation/PSReader/LegacyReaderConfiguration/shareTemplater-swift.property)

Optional share templater containing customized template strings for sharing content.

[`LegacyReaderConfiguration.ShareTemplater`](/documentation/PSReader/LegacyReaderConfiguration/ShareTemplater-swift.struct)

Defines templated strings for customizing sharing functionality within the legacy reader.

### Status Bar

[`prefersStatusBarHidden`](/documentation/PSReader/LegacyReaderConfiguration/prefersStatusBarHidden)

Controls whether the status bar is hidden in the legacy reader.

