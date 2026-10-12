<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ButtonConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19ButtonConfigurationV"
  },
  "title" : "ButtonConfiguration"
}
-->

# ButtonConfiguration

Configuration object used to customize buttons displayed within the SDK’s UI.

```
struct ButtonConfiguration
```

## Overview

Use this configuration to specify button positioning, size, spacing, tint color, and icons.

This configuration allows precise control over button placement relative to
view edges and other content, enabling you to match buttons to your application’s
design and interaction guidelines.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DismissHeaderViewController``

## Topics

### Creating a Dismiss Button

[`dismissButton(size:insets:position:tintColor:image:)`](/documentation/PSReader/ButtonConfiguration/dismissButton(size:insets:position:tintColor:image:))

Creates a preconfigured dismiss button suitable for use with [`DismissHeaderViewController`](/documentation/PSReader/DismissHeaderViewController).

### Appearance

[`image`](/documentation/PSReader/ButtonConfiguration/image)

Icon image displayed within the button.

[`tintColor`](/documentation/PSReader/ButtonConfiguration/tintColor)

Tint color applied to the button’s icon.

### Size and Position

[`size`](/documentation/PSReader/ButtonConfiguration/size)

The size of the button.

[`insets`](/documentation/PSReader/ButtonConfiguration/insets)

Edge insets defining internal padding around the button’s content.

[`position`](/documentation/PSReader/ButtonConfiguration/position-swift.property)

Specifies the button’s horizontal and vertical positioning within its containing view.

[`ButtonConfiguration.Position`](/documentation/PSReader/ButtonConfiguration/Position-swift.enum)

Defines positioning options for buttons within their containing view.

