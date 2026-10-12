<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderConfiguration/search",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19ReaderConfigurationV6searchAA06SearchC0VSgvp"
  },
  "title" : "search"
}
-->

# search

Optional search configuration enabling in-reader search.

```
var search: SearchConfiguration?
```

## Discussion

When set with a non-nil [`searchDelegate`](/documentation/PSReader/SearchConfiguration/searchDelegate), a search
option appears in the reader’s settings menu. Set to `nil` to disable
search entirely in the reader.

In carousel-based setups, this is initialized by default and the carousel
provides a default [`SearchDelegate`](/documentation/PSReader/SearchDelegate) automatically if one is not set.
For standalone view controllers (e.g., [`BookmarksViewController`](/documentation/PSReader/BookmarksViewController),
[`DownloadsViewController`](/documentation/PSReader/DownloadsViewController)), you must provide the delegate explicitly
using [`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate) or a custom implementation.