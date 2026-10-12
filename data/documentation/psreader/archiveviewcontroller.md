<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)ArchiveViewController"
  },
  "title" : "ArchiveViewController"
}
-->

# ArchiveViewController

A standalone view controller for displaying publication archives.

```
@MainActor class ArchiveViewController
```

## Overview

Use this view controller to embed an archive view within your app’s interface,
allowing users to browse and access different types of publication content including
editions on PageSuite’s current system (classic PDF and responsive alike),
legacy replica editions, and kiosk-style publication grids.

The view displays publications in a visual grid format and handles user interactions
such as selecting, opening, and managing publications.

Customize the appearance and behavior of this view through a provided [`ArchiveConfiguration`](/documentation/PSReader/ArchiveConfiguration)
object. By default, the view uses theming and settings defined by the supplied global configuration.

## Usage

```swift
let archive = ArchiveViewController(
    globalConfig: globalConfig,
    archiveType: .feedArchive(guid: "APP_GUID", publicationName: "Daily News")
)

navigationController?.pushViewController(archive, animated: true)
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Embedding-Prebuilt-Screens>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController``

## Topics

### Creating an Archive Screen

[`init(globalConfig:archiveConfig:archiveType:)`](/documentation/PSReader/ArchiveViewController/init(globalConfig:archiveConfig:archiveType:))

Initializes a new instance of the archive view controller with the provided configurations.

[`ArchiveViewController.ArchiveType`](/documentation/PSReader/ArchiveViewController/ArchiveType)

Describes the type of archive content to display.

