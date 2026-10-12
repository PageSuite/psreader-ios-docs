<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchResult",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12SearchResultV"
  },
  "title" : "SearchResult"
}
-->

# SearchResult

A single search result returned by the PageSuite search API.

```
struct SearchResult
```

## Overview

Each result represents an article or a page from an edition on PageSuite’s
current system, or a page from a legacy replica edition. Use the [`type`](/documentation/PSReader/SearchResult/type)
property to distinguish between result types:

- `"EDITION_ARTICLE"` for article results.
- `"EDITION_PAGE"` for page results.
- `"REPLICA_PAGE"` for legacy replica page results.

## Topics

### Identifying a Result

[`id`](/documentation/PSReader/SearchResult/id)

A locally generated unique identifier for this result.

[`type`](/documentation/PSReader/SearchResult/type)

The result type — [`editionArticleType`](/documentation/PSReader/SearchResult/editionArticleType), [`editionPageType`](/documentation/PSReader/SearchResult/editionPageType) or
[`replicaPageType`](/documentation/PSReader/SearchResult/replicaPageType).

[`editionArticleType`](/documentation/PSReader/SearchResult/editionArticleType)

[`type`](/documentation/PSReader/SearchResult/type) value for article results from editions on PageSuite’s
current system.

[`editionPageType`](/documentation/PSReader/SearchResult/editionPageType)

[`type`](/documentation/PSReader/SearchResult/type) value for page results from editions on PageSuite’s current
system.

### Locating the Content

[`editionId`](/documentation/PSReader/SearchResult/editionId)

The edition identifier.

[`pageId`](/documentation/PSReader/SearchResult/pageId)

The page identifier.

[`applicationId`](/documentation/PSReader/SearchResult/applicationId)

The application (publication) identifier.

[`publicationId`](/documentation/PSReader/SearchResult/publicationId)

The publication identifier.

[`publishedId`](/documentation/PSReader/SearchResult/publishedId)

The published content identifier.

[`accountId`](/documentation/PSReader/SearchResult/accountId)

The account identifier.

### Displaying a Result

[`headline`](/documentation/PSReader/SearchResult/headline)

The article headline.

[`section`](/documentation/PSReader/SearchResult/section)

The section name for article results.

[`author`](/documentation/PSReader/SearchResult/author)

The article author.

[`pageNumber`](/documentation/PSReader/SearchResult/pageNumber)

The page number for page results.

[`snippet`](/documentation/PSReader/SearchResult/snippet)

A text snippet with `<b>` tags highlighting matched terms.

[`formattedSnippet(font:)`](/documentation/PSReader/SearchResult/formattedSnippet(font:))

Returns the [`snippet`](/documentation/PSReader/SearchResult/snippet) as an attributed string with matched terms in bold.

[`parsedEditionDate`](/documentation/PSReader/SearchResult/parsedEditionDate)

The [`editionDate`](/documentation/PSReader/SearchResult/editionDate) parsed as a `Date`.

[`editionDate`](/documentation/PSReader/SearchResult/editionDate)

The edition date in ISO 8601 format. The backend may return this with
or without fractional seconds (`yyyy-MM-dd'T'HH:mm:ss.SSS'Z'` or
`yyyy-MM-dd'T'HH:mm:ss'Z'`). Use [`parsedEditionDate`](/documentation/PSReader/SearchResult/parsedEditionDate) to get a `Date`.

[`publicationName`](/documentation/PSReader/SearchResult/publicationName)

The publication name, populated client-side by matching [`applicationId`](/documentation/PSReader/SearchResult/applicationId)
against the list of [`SearchPublication`](/documentation/PSReader/SearchPublication) entries.

[`images`](/documentation/PSReader/SearchResult/images)

Images associated with the result.

[`SearchResult.Image`](/documentation/PSReader/SearchResult/Image)

An image associated with a search result.

[`content`](/documentation/PSReader/SearchResult/content)

The full article content.

### Replica Editions

[`replicaPageType`](/documentation/PSReader/SearchResult/replicaPageType)

[`type`](/documentation/PSReader/SearchResult/type) value for page results from legacy replica editions.

[`editionName`](/documentation/PSReader/SearchResult/editionName)

The edition name, populated for replica results only.

