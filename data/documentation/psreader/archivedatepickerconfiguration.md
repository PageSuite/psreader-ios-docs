<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveDatePickerConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader30ArchiveDatePickerConfigurationV"
  },
  "title" : "ArchiveDatePickerConfiguration"
}
-->

# ArchiveDatePickerConfiguration

Configuration object for customizing the appearance and behavior of the
archive date picker within the SDK.

```
struct ArchiveDatePickerConfiguration
```

## Overview

The archive date picker is an optional feature that enables users to filter
editions by selecting specific months from an archive view. When enabled, users
can tap a date selection button to open an overlay picker for month selection.

Use this configuration to align the date picker’s colors, fonts, labels, and
appearance with your application’s overall design.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/datePicker``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/ArchiveDatePickerConfiguration/init(globalConfig:))

Initializes a new date picker configuration using the provided global
SDK configuration for consistent theming and assets.

### Date Range

[`minimumDate`](/documentation/PSReader/ArchiveDatePickerConfiguration/minimumDate)

Optional minimum selectable date. Users will not be able to select dates earlier than this.

### Toggle Button

[`toggleButtonLabel`](/documentation/PSReader/ArchiveDatePickerConfiguration/toggleButtonLabel)

Label configuration for the toggle button that opens the date picker overlay.

[`toggleButtonBackgroundColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/toggleButtonBackgroundColor)

Background color of the toggle button.

### Date Button

[`dateButtonLabel`](/documentation/PSReader/ArchiveDatePickerConfiguration/dateButtonLabel)

Label configuration for the date selection button that displays the currently selected date.

[`dateButtonForegroundColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/dateButtonForegroundColor)

Text color of the date selection button.

[`dateButtonBackgroundColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/dateButtonBackgroundColor)

Background color of the date selection button.

### Clear Button

[`clearButtonForegroundColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/clearButtonForegroundColor)

Foreground (text/icon) color of the clear button.

[`clearButtonBackgroundColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/clearButtonBackgroundColor)

Background color for the clear button that resets the date filter to the latest available edition.

### Picker Overlay

[`overlayBackgroundColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/overlayBackgroundColor)

Background color of the overlay that appears when the date picker is active.

[`overlayDatePickerFont`](/documentation/PSReader/ArchiveDatePickerConfiguration/overlayDatePickerFont)

Font used within the overlay’s date picker wheel.

[`overlaySelectLabel`](/documentation/PSReader/ArchiveDatePickerConfiguration/overlaySelectLabel)

Label configuration for the “Select” button in the date picker overlay.

[`overlayCancelLabel`](/documentation/PSReader/ArchiveDatePickerConfiguration/overlayCancelLabel)

Label configuration for the “Cancel” button in the date picker overlay.

[`overlayDividerColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/overlayDividerColor)

Divider color within the date picker overlay.

### Colors and Icons

[`dividerColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/dividerColor)

Color of dividers separating UI elements within the date picker.

[`placeholderColor`](/documentation/PSReader/ArchiveDatePickerConfiguration/placeholderColor)

Color used as a placeholder during loading states within the date picker interface.

[`assetDelegate`](/documentation/PSReader/ArchiveDatePickerConfiguration/assetDelegate)

Delegate used to provide custom assets for the date picker, such as icons.

