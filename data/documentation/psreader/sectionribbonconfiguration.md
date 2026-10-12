<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SectionRibbonConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader26SectionRibbonConfigurationV"
  },
  "title" : "SectionRibbonConfiguration"
}
-->

# SectionRibbonConfiguration

Configuration object controlling the appearance and layout of the carousel section ribbon.

```
struct SectionRibbonConfiguration
```

## Overview

The section ribbon displays primary sections horizontally across the top of the
carousel interface, allowing users to navigate quickly between major content areas.

Customize this configuration to match your app’s design system, branding, and
preferred layout behavior.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselConfiguration``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/SectionRibbonConfiguration/init(globalConfig:))

Initializes a new `SectionRibbonConfiguration` using global SDK settings.

### Colors

[`backgroundColor`](/documentation/PSReader/SectionRibbonConfiguration/backgroundColor)

Background color of the section ribbon.

[`indicatorColor`](/documentation/PSReader/SectionRibbonConfiguration/indicatorColor)

Color of the indicator displayed beneath the selected section.

[`dividerColor`](/documentation/PSReader/SectionRibbonConfiguration/dividerColor)

Color of the divider line separating the ribbon from the content below.

### Section Titles

[`titleLabel`](/documentation/PSReader/SectionRibbonConfiguration/titleLabel)

Appearance configuration for section titles in their default (unselected) state.

[`selectedTitleLabel`](/documentation/PSReader/SectionRibbonConfiguration/selectedTitleLabel)

Appearance configuration for section titles when selected.

### Layout

[`layout`](/documentation/PSReader/SectionRibbonConfiguration/layout)

Layout mode controlling how section titles are horizontally arranged.

[`SectionRibbonConfiguration.LayoutMode`](/documentation/PSReader/SectionRibbonConfiguration/LayoutMode)

Determines how the section titles are laid out horizontally within the ribbon.

