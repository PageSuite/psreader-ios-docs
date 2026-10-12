<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DownloadsViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)DownloadsViewController"
  },
  "title" : "DownloadsViewController"
}
-->

# DownloadsViewController

A standalone view controller for displaying downloaded editions.

```
@MainActor class DownloadsViewController
```

## Overview

Use this view controller to embed a downloads view within your app’s interface,
allowing users to manage and view editions they have downloaded for offline reading.

The view displays a visual grid of downloaded editions from either system
and handles user interactions such as selecting, opening, and deleting editions.

Customize the appearance and behavior of this view through a provided [`DownloadsConfiguration`](/documentation/PSReader/DownloadsConfiguration)
object. By default, the view uses theming and settings defined by the supplied global configuration.

## Usage

```swift
let downloads = DownloadsViewController(
    globalConfig: globalConfig,
    downloadTypes: .all
)

navigationController?.pushViewController(downloads, animated: true)
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Downloads-and-Offline-Reading>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsConfiguration``

## Topics

### Creating the Screen

[`init(globalConfig:downloadsConfig:downloadTypes:)`](/documentation/PSReader/DownloadsViewController/init(globalConfig:downloadsConfig:downloadTypes:))

Initializes a new instance of the downloads view controller with the provided configurations.

### Sorting

[`sortMode`](/documentation/PSReader/DownloadsViewController/sortMode-swift.property)

The current sort mode for displaying downloaded editions.

[`DownloadsViewController.SortMode`](/documentation/PSReader/DownloadsViewController/SortMode-swift.enum)

Specifies the sort order for downloaded editions.

### Fitting the Screen Into Your Layout

[`additionalSafeAreaInsets`](/documentation/PSReader/DownloadsViewController/additionalSafeAreaInsets)

Extra insets the downloads grid keeps clear, on top of the safe area.

[`overrideUserInterfaceStyle`](/documentation/PSReader/DownloadsViewController/overrideUserInterfaceStyle)

Forces the downloads screen into light or dark mode.

