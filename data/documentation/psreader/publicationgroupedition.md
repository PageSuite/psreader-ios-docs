<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PublicationGroupEdition",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PublicationGroupEditionV"
  },
  "title" : "PublicationGroupEdition"
}
-->

# PublicationGroupEdition

The latest edition of one publication in a publication group.

```
struct PublicationGroupEdition
```

## Overview

[`PublicationGroupService`](/documentation/PSReader/PublicationGroupService) returns one of these per publication. It
identifies the edition and carries enough to show its cover; resolve the
full catalog entry with [`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:))
to open it.