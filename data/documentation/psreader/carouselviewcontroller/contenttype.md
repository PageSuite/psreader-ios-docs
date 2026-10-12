<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/ContentType",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC11ContentTypeO"
  },
  "title" : "CarouselViewController.ContentType"
}
-->

# CarouselViewController.ContentType

Describes the content type of a section or subsection page.

```
enum ContentType
```

## Overview

Each case represents a different content source that can be displayed within
the carousel. Choose between editions on PageSuite’s current system and
legacy replica editions depending on your publication’s backend system.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Edition-Platforms>

## Topics

### Archives and Kiosks

[`CarouselViewController.ContentType.feedArchive(guid:publicationName:config:)`](/documentation/PSReader/CarouselViewController/ContentType/feedArchive(guid:publicationName:config:))

An archive screen for editions on PageSuite’s current system,
classic PDF or responsive.

[`CarouselViewController.ContentType.feedPublicationKiosk(publications:config:)`](/documentation/PSReader/CarouselViewController/ContentType/feedPublicationKiosk(publications:config:))

A grid of publications on PageSuite’s current system, each linking
to its archive.

### Your Content

[`CarouselViewController.ContentType.bookmarks(type:config:)`](/documentation/PSReader/CarouselViewController/ContentType/bookmarks(type:config:))

A screen for local bookmarks.

[`CarouselViewController.ContentType.downloads(type:config:)`](/documentation/PSReader/CarouselViewController/ContentType/downloads(type:config:))

A screen for local downloads.

### Search

[`CarouselViewController.ContentType.search(config:)`](/documentation/PSReader/CarouselViewController/ContentType/search(config:))

A search screen.

### Replica Editions

[`CarouselViewController.ContentType.replicaArchive(guid:supplements:config:)`](/documentation/PSReader/CarouselViewController/ContentType/replicaArchive(guid:supplements:config:))

An archive screen for legacy replica editions.

[`CarouselViewController.ContentType.replicaPublicationKiosk(publications:config:)`](/documentation/PSReader/CarouselViewController/ContentType/replicaPublicationKiosk(publications:config:))

A grid of replica publications, each linking to a publication landing page.

