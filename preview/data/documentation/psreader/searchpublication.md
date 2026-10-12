<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchPublication",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17SearchPublicationV"
  },
  "title" : "SearchPublication"
}
-->

# SearchPublication

A publication that can be searched within using the PageSuite search API.

```
struct SearchPublication
```

## Overview

Each publication corresponds to an edition application on PageSuite’s
current system or a legacy replica publication, identified by a GUID.

## Topics

### Creating a Search Publication

[`init(title:guid:publishedDomain:searchType:)`](/documentation/PSReader/SearchPublication/init(title:guid:publishedDomain:searchType:))

Creates a new search publication.

### Identifying the Publication

[`guid`](/documentation/PSReader/SearchPublication/guid)

The publication GUID. A publication on PageSuite’s current system and
a legacy replica publication have distinct GUIDs; pair it with the
matching [`searchType`](/documentation/PSReader/SearchPublication/searchType).

[`searchType`](/documentation/PSReader/SearchPublication/searchType)

The publication type. Must match the type configured on the backend
for search to return results.

[`title`](/documentation/PSReader/SearchPublication/title)

The display name of the publication.

### Loading Editions

[`publishedDomain`](/documentation/PSReader/SearchPublication/publishedDomain)

The base domain used for loading edition content for this publication.

