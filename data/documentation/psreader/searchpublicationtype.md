<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchPublicationType",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21SearchPublicationTypeO"
  },
  "title" : "SearchPublicationType"
}
-->

# SearchPublicationType

The type of a searchable publication.

```
enum SearchPublicationType
```

## Overview

Publications on PageSuite’s current system are indexed differently on the
backend depending on their type. The correct value is required for search to return results, but
there is no other difference between the [`SearchPublicationType.app`](/documentation/PSReader/SearchPublicationType/app) and [`SearchPublicationType.publication`](/documentation/PSReader/SearchPublicationType/publication) types.

[`SearchPublicationType.replica`](/documentation/PSReader/SearchPublicationType/replica) marks a legacy replica publication. Replica publications are
searched through the legacy search endpoint: the publication GUID is
resolved to its latest edition, which is then searched with publication
scope. The two backends are never mixed — when the first publication
provided by a [`SearchDelegate`](/documentation/PSReader/SearchDelegate) is [`SearchPublicationType.replica`](/documentation/PSReader/SearchPublicationType/replica), all publications are
assumed to be replica and the legacy backend is used for every search.

## Topics

### Feed Publications

[`SearchPublicationType.app`](/documentation/PSReader/SearchPublicationType/app)

A publication on PageSuite’s current system, indexed as an app.

[`SearchPublicationType.publication`](/documentation/PSReader/SearchPublicationType/publication)

A publication on PageSuite’s current system, indexed as a
publication.

### Replica Editions

[`SearchPublicationType.replica`](/documentation/PSReader/SearchPublicationType/replica)

A publication on the legacy replica system, identified by its replica
publication GUID.

