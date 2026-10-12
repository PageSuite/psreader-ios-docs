<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/KioskReplicaPublication",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23KioskReplicaPublicationV"
  },
  "title" : "KioskReplicaPublication"
}
-->

# KioskReplicaPublication

Describes a replica publication entry in a kiosk grid.

```
struct KioskReplicaPublication
```

## Overview

Use [`archiveConfig`](/documentation/PSReader/KioskReplicaPublication/archiveConfig) to override archive styling or behavior for just this
publication. If [`archiveConfig`](/documentation/PSReader/KioskReplicaPublication/archiveConfig) is `nil`, the kiosk’s default configuration
is used.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/ContentType/replicaPublicationKiosk(publications:config:)``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController/ArchiveType/replicaPublicationKiosk(publications:)``

## Topics

### Creating a Kiosk Publication

[`init(guid:archiveConfig:)`](/documentation/PSReader/KioskReplicaPublication/init(guid:archiveConfig:))

Creates a replica publication entry for a kiosk grid.

### Identifying the Publication

[`guid`](/documentation/PSReader/KioskReplicaPublication/guid)

The publication guid used to load the replica archive.

### Customizing Its Archive

[`archiveConfig`](/documentation/PSReader/KioskReplicaPublication/archiveConfig)

Optional per-publication archive configuration override.

