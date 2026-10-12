<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultEditionDateFormatter",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultEditionDateFormatterV"
  },
  "title" : "DefaultEditionDateFormatter"
}
-->

# DefaultEditionDateFormatter

Default implementation of [`EditionDateFormatter`](/documentation/PSReader/EditionDateFormatter) using `DateFormatter`.

```
struct DefaultEditionDateFormatter
```

## Overview

This formatter uses standard date formatting to represent editions. It can be
customized with different formats and time zones. When no date is available,
it returns a placeholder (`"-"`).

For an edition, it formats [`editionDate`](/documentation/PSReader/PSEPublished/editionDate), the issue date on
the masthead, and falls back to [`datePublished`](/documentation/PSReader/PSEPublished/datePublished).

```swift
// Custom date format
let formatter = DefaultEditionDateFormatter(
    dateFormat: "dd MMM yyyy",
    timeZone: TimeZone(identifier: "Europe/London")!
)
```

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/EditionDateFormatter``

## Topics

### Creating a Formatter

[`init(dateFormat:timeZone:locale:)`](/documentation/PSReader/DefaultEditionDateFormatter/init(dateFormat:timeZone:locale:))

Initializes a new formatter with the given date format and time zone.

[`init(dateFormatter:)`](/documentation/PSReader/DefaultEditionDateFormatter/init(dateFormatter:))

Initializes a new formatter with a given `DateFormatter`.

[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter)

The date formatter that produces edition strings.

### Formatting Editions

[`string(for:)`](/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-28uwo)

Formats the edition’s [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) with
[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter), or its [`datePublished`](/documentation/PSReader/PSEPublished/datePublished) when it has
no edition date.

### Formatting Bookmarks and Search Results

[`string(for:)`](/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-4lxiv)

Formats the bookmarked edition’s [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) with
[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter), falling back to its [`datePublished`](/documentation/PSReader/PSEPublished/datePublished)
and then to the bookmark’s own [`editionDate`](/documentation/PSReader/PSEBookmarkPage/editionDate).

[`string(for:)`](/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-2kybo)

Formats the bookmarked edition’s [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) with
[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter), falling back to its [`datePublished`](/documentation/PSReader/PSEPublished/datePublished)
and then to the bookmark’s own [`editionDate`](/documentation/PSReader/PSEBookmarkArticle/editionDate).

[`string(for:)`](/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-5sjpw)

Formats the search result’s edition date.

### Replica Editions

[`string(for:)`](/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-639lb)

Formats the edition’s [`publishDate`](/documentation/PSReader/PSEdition/publishDate) with
[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter).

[`string(for:)`](/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-4azho)

Formats the bookmark’s edition date with [`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter).

[`string(for:)`](/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-37y9y)

Formats the bookmark’s edition date with [`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter).

