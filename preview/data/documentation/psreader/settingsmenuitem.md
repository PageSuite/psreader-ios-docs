<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsMenuItem",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16SettingsMenuItemV"
  },
  "title" : "SettingsMenuItem"
}
-->

# SettingsMenuItem

A row your app adds to the reader’s settings menu.

```
struct SettingsMenuItem
```

## Overview

Additional items follow the built-in settings, in the order given.
Tapping one calls its handler with a [`SettingsMenuContext`](/documentation/PSReader/SettingsMenuContext), which
presents over the menu or closes it.

Each reader has its own settings, so set the items on one
[`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) and share it between the readers that should
show them:

```swift
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.settings.additionalItems = [
    SettingsMenuItem(title: "Help", image: UIImage(systemName: "questionmark.circle")) { context in
        context.present(HelpViewController())
    }
]

archiveConfig.readerConfig = readerConfig
bookmarksConfig.readerConfig = readerConfig
downloadsConfig.readerConfig = readerConfig
```

The legacy replica reader doesn’t show additional items.

For a complete example, see [Adding Your Own Rows](/documentation/PSReader/Customizing-the-Reader-Screen#Adding-Your-Own-Rows).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/additionalItems``

## Topics

### Creating an Item

[`init(title:image:role:handler:)`](/documentation/PSReader/SettingsMenuItem/init(title:image:role:handler:))

Creates a settings menu item.

### Appearance

[`title`](/documentation/PSReader/SettingsMenuItem/title)

The item’s title.

[`image`](/documentation/PSReader/SettingsMenuItem/image)

An icon shown before the title, drawn as a template in the menu’s icon color.

[`role`](/documentation/PSReader/SettingsMenuItem/role-swift.property)

How the item is styled.

[`SettingsMenuItem.Role`](/documentation/PSReader/SettingsMenuItem/Role-swift.enum)

How an item is styled.

### Handling Taps

[`handler`](/documentation/PSReader/SettingsMenuItem/handler)

Called on the main thread when the item is tapped.

