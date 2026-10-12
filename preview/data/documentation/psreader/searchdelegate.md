<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14SearchDelegateP"
  },
  "title" : "SearchDelegate"
}
-->

# SearchDelegate

A delegate that provides the list of searchable publications and their reader configurations.

```
protocol SearchDelegate
```

## Overview

Implement this protocol to control which publications appear in the search interface
and how search results are opened in the reader.

The SDK provides [`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate) as a ready-made implementation
that derives publications from a `PSAppConfig` or a remote shortcode.

To set up the prebuilt search screen, see [Search](/documentation/PSReader/Search).

## Topics

### Supplying Publications

[`searchPublications(completion:)`](/documentation/PSReader/SearchDelegate/searchPublications(completion:))

Provides the list of publications available for searching.

### Opening Results

[`searchReaderConfiguration(for:)`](/documentation/PSReader/SearchDelegate/searchReaderConfiguration(for:))

Returns the reader configuration to use when opening a search result from the given publication.

