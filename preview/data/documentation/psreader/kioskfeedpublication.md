<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/KioskFeedPublication",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20KioskFeedPublicationV"
  },
  "title" : "KioskFeedPublication"
}
-->

# KioskFeedPublication

Describes an entry in a kiosk grid of publications on PageSuite’s current
system.

```
struct KioskFeedPublication
```

## Overview

Use [`archiveConfig`](/documentation/PSReader/KioskFeedPublication/archiveConfig) to override archive styling or behavior for just this
publication. If [`archiveConfig`](/documentation/PSReader/KioskFeedPublication/archiveConfig) is `nil`, the kiosk’s default configuration
is used.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/ContentType/feedPublicationKiosk(publications:config:)``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController/ArchiveType/feedPublicationKiosk(publications:)``

## Topics

### Creating a Kiosk Publication

[`init(name:guid:archiveConfig:)`](/documentation/PSReader/KioskFeedPublication/init(name:guid:archiveConfig:))

Creates a publication entry for a kiosk grid.

### Identifying the Publication

[`name`](/documentation/PSReader/KioskFeedPublication/name)

The display name for the publication.

[`guid`](/documentation/PSReader/KioskFeedPublication/guid)

The publication GUID used to load the publication’s archive.

### Customizing Its Archive

[`archiveConfig`](/documentation/PSReader/KioskFeedPublication/archiveConfig)

Optional per-publication archive configuration override.

