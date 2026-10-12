<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ArchiveConfigurationV"
  },
  "title" : "ArchiveConfiguration"
}
-->

# ArchiveConfiguration

Configuration for customizing the appearance and behavior of publication archive views.

```
struct ArchiveConfiguration
```

## Overview

The archive screen lists editions available for viewing or downloading.
This configuration lets you define visual styles, default behaviors, and
error messaging tailored to your app’s design requirements.

The nested [`readerConfig`](/documentation/PSReader/ArchiveConfiguration/readerConfig) property controls the reader presented when an
edition is opened from this archive. Customize it to adjust reader-specific
appearance without affecting the archive itself.

To place an archive screen in your own navigation, see
[Embedding Prebuilt Screens](/documentation/PSReader/Embedding-Prebuilt-Screens).

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Theming>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/ArchiveConfiguration/init(globalConfig:))

Initializes an `ArchiveConfiguration` using the provided global configuration.

### Appearance

[`backgroundColor`](/documentation/PSReader/ArchiveConfiguration/backgroundColor)

Background color displayed behind the entire archive view.

[`placeholderColor`](/documentation/PSReader/ArchiveConfiguration/placeholderColor)

Color displayed as a placeholder while content is loading.

[`maxContentWidth`](/documentation/PSReader/ArchiveConfiguration/maxContentWidth)

Maximum width of the archive content in regular width environments.

### Edition Thumbnails

[`cellAspectRatio`](/documentation/PSReader/ArchiveConfiguration/cellAspectRatio)

Aspect ratio for thumbnails representing editions in the archive view.

[`thumbnailContentMode`](/documentation/PSReader/ArchiveConfiguration/thumbnailContentMode)

Content mode for standard archive thumbnails.

[`latestPaperThumbnailContentMode`](/documentation/PSReader/ArchiveConfiguration/latestPaperThumbnailContentMode)

Optional content mode override for the latest edition hero cell.

### Edition Labels

[`latestPaperTitleLabel`](/documentation/PSReader/ArchiveConfiguration/latestPaperTitleLabel)

Configuration for the title label of the latest edition (“Latest Paper”).

[`titleLabel`](/documentation/PSReader/ArchiveConfiguration/titleLabel)

Configuration for regular edition title labels within the archive.

[`dateFormatter`](/documentation/PSReader/ArchiveConfiguration/dateFormatter)

Formatter responsible for providing display strings for edition dates.

### Download Button

[`downloadButtonEnabled`](/documentation/PSReader/ArchiveConfiguration/downloadButtonEnabled)

Indicates whether the download button is enabled and visible in the archive.

[`downloadButtonColor`](/documentation/PSReader/ArchiveConfiguration/downloadButtonColor)

Color of the download button icon shown on editions.

### Choosing Editions

[`archiveLimit`](/documentation/PSReader/ArchiveConfiguration/archiveLimit)

Maximum number of editions displayed in the archive.

[`datePicker`](/documentation/PSReader/ArchiveConfiguration/datePicker)

Optional configuration for displaying a date picker to filter archived editions.

[`feedPublicationType`](/documentation/PSReader/ArchiveConfiguration/feedPublicationType-swift.property)

The backend that serves this archive’s editions when filtering by
[`datePicker`](/documentation/PSReader/ArchiveConfiguration/datePicker).

[`ArchiveConfiguration.FeedPublicationType`](/documentation/PSReader/ArchiveConfiguration/FeedPublicationType-swift.enum)

Identifies which backend serves the editions of an archive on
PageSuite’s current system by date.

### Errors

[`errorTitleLabel`](/documentation/PSReader/ArchiveConfiguration/errorTitleLabel)

Configuration for the primary error message title displayed when content fails to load.

[`errorSubtitleLabel`](/documentation/PSReader/ArchiveConfiguration/errorSubtitleLabel)

Configuration for the secondary error message subtitle displayed when content fails to load.
Use this to provide additional details.

### Opening Editions

[`readerConfig`](/documentation/PSReader/ArchiveConfiguration/readerConfig)

Configuration applied to the reader view presented when editions are opened.

[`publishedDomain`](/documentation/PSReader/ArchiveConfiguration/publishedDomain)

Base domain used for loading edition content.

### Searching Editions

[`searchPublicationType`](/documentation/PSReader/ArchiveConfiguration/searchPublicationType)

The publication type used when searching this publication’s content.

### Replica Editions

[`supplementsTitleLabel`](/documentation/PSReader/ArchiveConfiguration/supplementsTitleLabel)

Configuration for supplements ribbon title.

[`supplementsBackgroundColor`](/documentation/PSReader/ArchiveConfiguration/supplementsBackgroundColor)

Background color displayed behind the supplements section view.

