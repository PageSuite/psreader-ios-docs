<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished"
  },
  "title" : "PSEPublished"
}
-->

# PSEPublished

A published edition in a publication’s catalog — the unit an archive
lists and everything else opens.

```
@objc class PSEPublished
```

## Overview

[`FeedEditionService`](/documentation/PSReader/FeedEditionService) returns these grouped into [`PSEPublishedDate`](/documentation/PSReader/PSEPublishedDate)s.
A published edition is a lightweight manifest pointer: draw archive cells
from [`image`](/documentation/PSReader/PSEPublished/image), [`name`](/documentation/PSReader/PSEPublished/name), and [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) (the date
[`DefaultEditionDateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter) shows), then open its content
with [`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)), queue it for offline reading
with [`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager), or fetch the full page model via
[`edition(for:)`](/documentation/PSReader/FeedEditionService/edition(for:)). Property names mirror the backend
payload and are part of the shipped contract.

For how the catalog and content models fit together, see
[The Edition Model](/documentation/PSReader/The-Edition-Model).

## Topics

### Identity

[`publishedGUID`](/documentation/PSReader/PSEPublished/publishedGUID)

Unique identifier of this published edition — the identity that
downloads, bookmarks, and reading state key on.

[`editionGUID`](/documentation/PSReader/PSEPublished/editionGUID)

Identifier of the edition content behind this catalog entry.

[`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID)

GUID of the publication this edition belongs to. The property
keeps the identifier’s historical name; the docs call it the
publication GUID.

[`publicationGUID`](/documentation/PSReader/PSEPublished/publicationGUID)

GUID of the publication the backend files this edition’s content
under, read from the catalog payload.

[`accountGUID`](/documentation/PSReader/PSEPublished/accountGUID)

GUID of the PageSuite account that publishes this edition, as sent in
the catalog payload.

### Display

[`name`](/documentation/PSReader/PSEPublished/name)

The edition’s display name.

[`publicationName`](/documentation/PSReader/PSEPublished/publicationName)

The publication’s display name.

[`image`](/documentation/PSReader/PSEPublished/image)

URL of the cover thumbnail — the image to draw in archive grids.

[`datePublished`](/documentation/PSReader/PSEPublished/datePublished)

When the edition was published.

[`editionDate`](/documentation/PSReader/PSEPublished/editionDate)

The edition’s nominal date (the issue date on the masthead).

[`editionDateString`](/documentation/PSReader/PSEPublished/editionDateString)

The edition date as display text, for example
“Tuesday September 1 2026”.

[`useCustomEditionName`](/documentation/PSReader/PSEPublished/useCustomEditionName)

Whether the publisher chose to label this edition by its [`name`](/documentation/PSReader/PSEPublished/name)
rather than its date.

[`isSupplement`](/documentation/PSReader/PSEPublished/isSupplement)

Whether this edition is a supplement rather than a main edition.

### Opening

[`isAvailableToOpen`](/documentation/PSReader/PSEPublished/isAvailableToOpen)

Whether this edition can currently be opened from its own source:
true if a downloaded copy exists or the device is online.

[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:))

Opens a reader-ready source for this edition: the downloaded copy if
there is one, otherwise a network stream.

### Download Size and Freshness

[`totalSize`](/documentation/PSReader/PSEPublished/totalSize)

The size of the edition’s downloadable content in bytes, as reported
by the backend.

[`lastUpdatedTimestamp`](/documentation/PSReader/PSEPublished/lastUpdatedTimestamp)

A Unix timestamp of the edition’s last update, as sent by the
backend.

### Migrated Editions

[`isBridged`](/documentation/PSReader/PSEPublished/isBridged)

Whether this edition is a download migrated from the legacy SDK.

### Archive Dates

[`PSEPublishedDate`](/documentation/PSReader/PSEPublishedDate)

One calendar date in a publication’s archive, with the editions
published on it.

