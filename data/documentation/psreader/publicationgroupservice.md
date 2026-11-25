<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PublicationGroupService",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PublicationGroupServiceV"
  },
  "title" : "PublicationGroupService"
}
-->

# PublicationGroupService

Lists the publications in a publication group.

```
struct PublicationGroupService
```

## Overview

A publication group is a set of publications defined in PageSuite, such
as a newspaper’s supplements. Pass a group’s GUID to get the latest
edition of each publication in it, for a row of supplement covers for
example. The prebuilt archive does this for the groups you name in
[`CarouselViewController.ContentType.feedArchive(guid:publicationName:supplements:config:)`](/documentation/PSReader/CarouselViewController/ContentType/feedArchive(guid:publicationName:supplements:config:)).

```swift
let service = PublicationGroupService()
let supplements = try await service.latestEditions(groupGUID: "GROUP_GUID")

for supplement in supplements {
    let published = try await feedEditionService.published(forEditionGUID: supplement.editionGUID)
    published.applicationGUID = supplement.publicationGUID
    published.publicationName = supplement.publicationName
}
```

The group must hold publications on PageSuite’s current system; a group
of legacy replica publications, or an unknown GUID, returns an empty
list.