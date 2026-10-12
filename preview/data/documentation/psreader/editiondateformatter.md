<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EditionDateFormatter",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20EditionDateFormatterP"
  },
  "title" : "EditionDateFormatter"
}
-->

# EditionDateFormatter

A protocol defining methods for generating display strings to represent editions.

```
protocol EditionDateFormatter
```

## Overview

Implement this protocol to customize how editions are named or represented in
the UI. Although commonly editions are represented using formatted dates,
implementers may use alternative naming strategies such as edition names,
identifiers, or any other custom labeling approach.

To change how the prebuilt UI names editions, see [Theming](/documentation/PSReader/Theming).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultEditionDateFormatter``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/dateFormatter``

## Topics

### Formatting Editions

[`string(for:)`](/documentation/PSReader/EditionDateFormatter/string(for:)-3u5s)

Provides a formatted string representation for the given edition.

### Formatting Bookmarks and Search Results

[`string(for:)`](/documentation/PSReader/EditionDateFormatter/string(for:)-lbzz)

Provides a formatted string representation for a bookmarked page.

[`string(for:)`](/documentation/PSReader/EditionDateFormatter/string(for:)-6syu7)

Provides a formatted string representation for a bookmarked article.

[`string(for:)`](/documentation/PSReader/EditionDateFormatter/string(for:)-8s11v)

Provides a formatted string representation for the given search result’s edition date.

### Replica Editions

[`string(for:)`](/documentation/PSReader/EditionDateFormatter/string(for:)-6flyk)

Provides a formatted string representation for the given legacy
replica edition.

[`string(for:)`](/documentation/PSReader/EditionDateFormatter/string(for:)-2wbes)

Provides a formatted string representation for a bookmarked page
from a legacy replica edition.

[`string(for:)`](/documentation/PSReader/EditionDateFormatter/string(for:)-946ke)

Provides a formatted string representation for a bookmarked article
from a legacy replica edition.

