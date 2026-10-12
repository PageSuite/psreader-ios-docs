<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SubsectionRibbonConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29SubsectionRibbonConfigurationV"
  },
  "title" : "SubsectionRibbonConfiguration"
}
-->

# SubsectionRibbonConfiguration

Configuration used to customize the appearance and layout of the carousel subsection ribbon.

```
struct SubsectionRibbonConfiguration
```

## Overview

The subsection ribbon allows users to navigate subsections within a parent section.
It is displayed conditionally when subsections are available.

Use this configuration to align the subsection ribbon’s appearance and behavior with
your application’s design standards and branding.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselConfiguration``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/SubsectionRibbonConfiguration/init(globalConfig:))

Initializes a new `SubsectionRibbonConfiguration` using global SDK theming.

### Ribbon

[`ribbonBackgroundColor`](/documentation/PSReader/SubsectionRibbonConfiguration/ribbonBackgroundColor)

Background color of the subsection ribbon.

[`liquidGlassPolicy`](/documentation/PSReader/SubsectionRibbonConfiguration/liquidGlassPolicy)

Liquid Glass policy for the subsection ribbon.

### Pills

[`pillBackgroundColor`](/documentation/PSReader/SubsectionRibbonConfiguration/pillBackgroundColor)

Background color for each subsection item (“pill”) in its unselected state.

[`selectedPillBackgroundColor`](/documentation/PSReader/SubsectionRibbonConfiguration/selectedPillBackgroundColor)

Background color for a selected subsection item (“pill”).

[`titleLabel`](/documentation/PSReader/SubsectionRibbonConfiguration/titleLabel)

Configuration for subsection item titles in their default (unselected) state.

[`selectedTitleLabel`](/documentation/PSReader/SubsectionRibbonConfiguration/selectedTitleLabel)

Appearance configuration for subsection titles when selected.

### Layout

[`alignment`](/documentation/PSReader/SubsectionRibbonConfiguration/alignment-swift.property)

Horizontal alignment of subsection items within the ribbon.

[`SubsectionRibbonConfiguration.Alignment`](/documentation/PSReader/SubsectionRibbonConfiguration/Alignment-swift.enum)

Alignment options for subsection titles within the ribbon.

