<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveViewController/ArchiveType",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21ArchiveViewControllerC0B4TypeO"
  },
  "title" : "ArchiveViewController.ArchiveType"
}
-->

# ArchiveViewController.ArchiveType

Describes the type of archive content to display.

```
enum ArchiveType
```

## Overview

This mirrors [`CarouselViewController.ContentType`](/documentation/PSReader/CarouselViewController/ContentType) but is designed
for standalone use outside the carousel.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/ContentType``

## Topics

### Archives and Kiosks

[`ArchiveViewController.ArchiveType.feedArchive(guid:publicationName:)`](/documentation/PSReader/ArchiveViewController/ArchiveType/feedArchive(guid:publicationName:))

An archive screen for editions on PageSuite’s current system,
classic PDF or responsive.

[`ArchiveViewController.ArchiveType.feedPublicationKiosk(publications:)`](/documentation/PSReader/ArchiveViewController/ArchiveType/feedPublicationKiosk(publications:))

A grid of publications on PageSuite’s current system, each linking
to a publication landing page.

### Replica Editions

[`ArchiveViewController.ArchiveType.replicaArchive(guid:)`](/documentation/PSReader/ArchiveViewController/ArchiveType/replicaArchive(guid:))

An archive screen for legacy replica editions.

[`ArchiveViewController.ArchiveType.replicaPublicationKiosk(publications:)`](/documentation/PSReader/ArchiveViewController/ArchiveType/replicaPublicationKiosk(publications:))

A grid of replica publications, each linking to a publication landing page.

