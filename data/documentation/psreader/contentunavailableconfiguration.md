<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ContentUnavailableConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader31ContentUnavailableConfigurationV"
  },
  "title" : "ContentUnavailableConfiguration"
}
-->

# ContentUnavailableConfiguration

Configuration for customizing the appearance and behavior of content unavailable screens.

```
struct ContentUnavailableConfiguration
```

## Overview

Content unavailable screens are displayed when views such as Bookmarks
or Downloads have no content to present. It includes an icon, title, and
description providing guidance or context to the user.

Use this configuration to align the appearance of the no-content state with
your application’s visual style, colors, fonts, and overall user experience.

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/ContentUnavailableConfiguration/init(globalConfig:))

Initializes a new content-unavailable configuration using defaults from the global SDK configuration.

### Image

[`image`](/documentation/PSReader/ContentUnavailableConfiguration/image)

Optional image to display on the no-content screen.

[`imageSize`](/documentation/PSReader/ContentUnavailableConfiguration/imageSize)

The size of the icon displayed on the no-content screen.

[`tintColor`](/documentation/PSReader/ContentUnavailableConfiguration/tintColor)

Tint color applied to icons displayed within the no-content screen.

### Text

[`titleLabel`](/documentation/PSReader/ContentUnavailableConfiguration/titleLabel)

Configuration for the title label displayed on the no-content screen.

[`descriptionLabel`](/documentation/PSReader/ContentUnavailableConfiguration/descriptionLabel)

Configuration for the descriptive text providing additional guidance or information to the user.

### Background

[`backgroundColor`](/documentation/PSReader/ContentUnavailableConfiguration/backgroundColor)

Background color of the no-content view.

