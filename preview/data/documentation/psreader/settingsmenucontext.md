<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsMenuContext",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19SettingsMenuContextC"
  },
  "title" : "SettingsMenuContext"
}
-->

# SettingsMenuContext

Lets a settings menu item’s handler present over the menu, or close the
menu and the reader beneath it.

```
@MainActor final class SettingsMenuContext
```

## Overview

A context acts only while the menu it was made for is on screen. Once the
menu has gone, its methods do nothing.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsMenuItem``

## Topics

### Presenting Over the Menu

[`present(_:animated:completion:)`](/documentation/PSReader/SettingsMenuContext/present(_:animated:completion:))

Presents a view controller, such as a confirmation alert, over the
settings menu.

### Closing the Menu

[`dismissSettings(animated:completion:)`](/documentation/PSReader/SettingsMenuContext/dismissSettings(animated:completion:))

Closes the settings menu, leaving the reader open.

[`dismissReader(animated:completion:)`](/documentation/PSReader/SettingsMenuContext/dismissReader(animated:completion:))

Closes the settings menu and the reader beneath it, returning to
whatever opened the reader.

