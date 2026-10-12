<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEEdition"
  },
  "title" : "PSEEdition"
}
-->

# PSEEdition

The loaded content of an edition: its pages, precomputed spreads, and
sections.

```
@objc class PSEEdition
```

## Overview

You get one by opening a [`PSEEditionSource`](/documentation/PSReader/PSEEditionSource) (its
[`edition`](/documentation/PSReader/PSEEditionSource/edition) property) or directly from
[`edition(for:)`](/documentation/PSReader/FeedEditionService/edition(for:)). Property names mirror the backend
payload and are part of the shipped contract, casing included.

For how the catalog and content models fit together, see
[The Edition Model](/documentation/PSReader/The-Edition-Model).

## Topics

### Identity

[`editionguid`](/documentation/PSReader/PSEEdition/editionguid)

The edition GUID: the same value as [`editionGUID`](/documentation/PSReader/PSEPublished/editionGUID) on
the catalog entry this edition was opened from.

[`applicationguid`](/documentation/PSReader/PSEEdition/applicationguid)

GUID of the publication this edition belongs to, when the
edition payload includes it.

### Display

[`name`](/documentation/PSReader/PSEEdition/name)

The edition’s display name.

[`editionDateString`](/documentation/PSReader/PSEEdition/editionDateString)

The edition date as display text, for example
“Tuesday September 1 2026”.

[`editionDate`](/documentation/PSReader/PSEEdition/editionDate)

The edition’s date, parsed from [`pubdate`](/documentation/PSReader/PSEEdition/pubdate).

[`pubdate`](/documentation/PSReader/PSEEdition/pubdate)

The publication date string, as delivered by the backend.

[`image`](/documentation/PSReader/PSEEdition/image)

URL of the edition’s cover image, when the edition payload includes
one.

### Content

[`pages`](/documentation/PSReader/PSEEdition/pages)

Every page of the edition in reading order.

[`page(forGUID:)`](/documentation/PSReader/PSEEdition/page(forGUID:))

The first page whose `pageguid` matches, or nil.

[`pagesHaveArticles()`](/documentation/PSReader/PSEEdition/pagesHaveArticles())

Whether any page is an article page.

[`isReplicaEdition()`](/documentation/PSReader/PSEEdition/isReplicaEdition())

Whether the edition is a classic PDF edition, whose PDF pages pair
into double spreads, rather than a responsive one.

### Spreads

[`pageSpreads(for:)`](/documentation/PSReader/PSEEdition/pageSpreads(for:))

The spread list for a paging mode. Spread indices in
[`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) index into this array.

[`pageSpread(atIndex:pagingMode:)`](/documentation/PSReader/PSEEdition/pageSpread(atIndex:pagingMode:))

The spread at a spread index for a paging mode, or `nil` if out of
range.

[`pageIndex(for:inPagingMode:)`](/documentation/PSReader/PSEEdition/pageIndex(for:inPagingMode:))

The spread index presenting `page` in a paging mode, or `nil` if the
page isn’t in the edition.

[`pagesSingle`](/documentation/PSReader/PSEEdition/pagesSingle)

The spreads the reader pages between in single-page mode.

[`pagesDouble`](/documentation/PSReader/PSEEdition/pagesDouble)

The spreads the reader pages between in double-page mode.

### Sections

[`sections`](/documentation/PSReader/PSEEdition/sections)

The edition’s sections (news, sport, …) with their articles.

[`pageBrowserSections`](/documentation/PSReader/PSEEdition/pageBrowserSections)

Groupings used to build a sectioned page-browser UI.

[`PSESection`](/documentation/PSReader/PSESection)

A named section of an edition (news, sport, …) grouping its articles.

