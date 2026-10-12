<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublishedDate",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublishedDate"
  },
  "title" : "PSEPublishedDate"
}
-->

# PSEPublishedDate

One calendar date in a publication’s archive, with the editions
published on it.

```
@objc class PSEPublishedDate
```

## Overview

[`publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:)`](/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:publishedDomain:usesCache:))
returns these newest-first — which makes drawing a dated archive a
straight mapping, and gives `[PSEPublishedDate].latestEdition` its
meaning.

## Topics

### Reading a Date Group

[`date`](/documentation/PSReader/PSEPublishedDate/date)

The calendar date, as formatted by the backend.

[`editions`](/documentation/PSReader/PSEPublishedDate/editions)

The editions published on this date, in the order the backend lists
them.

### Creating a Date Group

[`init(date:editions:)`](/documentation/PSReader/PSEPublishedDate/init(date:editions:))

Creates a date group from a date string and the editions published
on it.

