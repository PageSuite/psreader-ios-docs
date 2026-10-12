<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)SearchViewController"
  },
  "title" : "SearchViewController"
}
-->

# SearchViewController

A standalone view controller for searching edition content.

```
@MainActor class SearchViewController
```

## Overview

The search view controller presents an interface where users can search
across one or more publications. For publications on PageSuite’s current system, results
include articles and pages, with support for filtering by type and
publication. For legacy replica publications, results are pages within a
single publication.

A [`SearchDelegate`](/documentation/PSReader/SearchDelegate) supplies the list of searchable publications and
provides reader configurations for opening search results. The type of the
first publication decides the search backend — publications on
PageSuite’s current system and legacy replica publications are never
mixed.

## Usage

```swift
let delegate = ApplicationSearchDelegate(
    shortcode: "SHORTCODE",
    readerConfig: readerConfig
)

let search = SearchViewController(
    globalConfig: globalConfig,
    delegate: delegate
)

navigationController?.pushViewController(search, animated: true)
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Search>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchConfiguration``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchDelegate``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ApplicationSearchDelegate``

## Topics

### Creating a Search Screen

[`init(globalConfig:searchConfig:delegate:dismissible:)`](/documentation/PSReader/SearchViewController/init(globalConfig:searchConfig:delegate:dismissible:))

Initializes a new standalone search view controller.

### Customizing the Screen

[`overrideUserInterfaceStyle`](/documentation/PSReader/SearchViewController/overrideUserInterfaceStyle)

Forces the search screen into light or dark mode.

