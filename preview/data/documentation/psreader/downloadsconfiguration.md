<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DownloadsConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22DownloadsConfigurationV"
  },
  "title" : "DownloadsConfiguration"
}
-->

# DownloadsConfiguration

Configuration for customizing the appearance and behavior of download archives.

```
struct DownloadsConfiguration
```

## Overview

The downloads view displays editions that users have downloaded for offline reading.
Downloads are displayed in a grid layout, showing thumbnails and associated metadata.

Use this configuration to customize the download interface, including thumbnail display,
colors, labels, and behaviors, ensuring visual consistency and a cohesive user experience.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Downloads-and-Offline-Reading>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsViewController``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/DownloadsConfiguration/init(globalConfig:))

Initializes a new downloads configuration with defaults provided by the global SDK configuration object.

### Choosing Editions

[`DownloadsConfiguration.DownloadType`](/documentation/PSReader/DownloadsConfiguration/DownloadType)

Defines the types of downloadable content supported by the downloads view.

### Appearance

[`backgroundColor`](/documentation/PSReader/DownloadsConfiguration/backgroundColor)

Background color of the downloads view.

[`placeholderColor`](/documentation/PSReader/DownloadsConfiguration/placeholderColor)

Placeholder color displayed during content loading states within the downloads view.

### Thumbnails

[`aspectRatio`](/documentation/PSReader/DownloadsConfiguration/aspectRatio)

Aspect ratio for thumbnails displayed in the downloads view.

[`thumbnailContentMode`](/documentation/PSReader/DownloadsConfiguration/thumbnailContentMode)

Content mode determining how bookmark thumbnails scale and fit within their containers.

### Rows

[`titleLabel`](/documentation/PSReader/DownloadsConfiguration/titleLabel)

Appearance configuration for the edition title labels displayed within each downloadable edition cell.

[`dateLabel`](/documentation/PSReader/DownloadsConfiguration/dateLabel)

Label configuration for displaying download dates.

[`dateFormatter`](/documentation/PSReader/DownloadsConfiguration/dateFormatter)

Formatter used to generate display strings for edition dates or names in the downloads view.

[`downloadIconColor`](/documentation/PSReader/DownloadsConfiguration/downloadIconColor)

Tint color used for download-related icons within the interface.

[`rowDividerColor`](/documentation/PSReader/DownloadsConfiguration/rowDividerColor)

Color of the divider line displayed between download rows.

### Sort Button

[`sortButtonLabel`](/documentation/PSReader/DownloadsConfiguration/sortButtonLabel)

Label configuration for the toggle button that opens the sort Selection button.

[`sortButtonBackgroundColor`](/documentation/PSReader/DownloadsConfiguration/sortButtonBackgroundColor)

Background color of the sort selection button.

### Empty State

[`noContentConfig`](/documentation/PSReader/DownloadsConfiguration/noContentConfig)

Configuration for the state displayed when no downloadable content is available.

### Opening Editions

[`readerConfig`](/documentation/PSReader/DownloadsConfiguration/readerConfig)

Reader configuration applied when opening downloaded content.

