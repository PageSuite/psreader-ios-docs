<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19SearchConfigurationV"
  },
  "title" : "SearchConfiguration"
}
-->

# SearchConfiguration

Configuration for the SDK’s built-in search interface.

```
struct SearchConfiguration
```

## Overview

Controls the appearance and behavior of the search view, including typography,
colors, filter pills, result cells, and error states. The search view is
presented from the reader’s settings menu or as a tab in the carousel.

Set [`searchDelegate`](/documentation/PSReader/SearchConfiguration/searchDelegate) to provide the list of searchable publications and
their reader configurations. Without a delegate, search will not be available.

> Note: Publications on PageSuite’s current system and legacy replica
> publications can’t be searched together. All the publications the
> ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchConfiguration/searchDelegate`` provides must be on the same edition system, and
> legacy replica search returns pages only.

To set up search in the prebuilt UI, see [Search](/documentation/PSReader/Search).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchDelegate``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ApplicationSearchDelegate``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchService``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/SearchConfiguration/init(globalConfig:))

Initializes a new `SearchConfiguration` using global SDK theming.

### Choosing What to Search

[`searchDelegate`](/documentation/PSReader/SearchConfiguration/searchDelegate)

The delegate that provides searchable publications and reader configurations.

[`accountGUID`](/documentation/PSReader/SearchConfiguration/accountGUID)

The account GUID the search view searches within and opens results
from.

[`timeZone`](/documentation/PSReader/SearchConfiguration/timeZone)

The time zone the search view passes to search requests and to the
reader when it opens a result from an edition on PageSuite’s current
system.

### Header and Search Field

[`backgroundColor`](/documentation/PSReader/SearchConfiguration/backgroundColor)

Background color of the search header.

[`searchBarBackgroundColor`](/documentation/PSReader/SearchConfiguration/searchBarBackgroundColor)

Background color of the search text field.

[`assetDelegate`](/documentation/PSReader/SearchConfiguration/assetDelegate)

Delegate providing custom images used within the search view.

[`liquidGlassPolicy`](/documentation/PSReader/SearchConfiguration/liquidGlassPolicy)

Liquid Glass policy for the search header.

### Filter Pills

[`pillBackgroundColor`](/documentation/PSReader/SearchConfiguration/pillBackgroundColor)

Background color for filter pills in their unselected state.

[`selectedPillBackgroundColor`](/documentation/PSReader/SearchConfiguration/selectedPillBackgroundColor)

Background color for the selected filter pill.

[`titleLabel`](/documentation/PSReader/SearchConfiguration/titleLabel)

Label configuration for unselected pill titles.

[`selectedTitleLabel`](/documentation/PSReader/SearchConfiguration/selectedTitleLabel)

Label configuration for the selected pill title.

### Results

[`resultsLabel`](/documentation/PSReader/SearchConfiguration/resultsLabel)

Label configuration for the results count label.

[`resultTitleLabel`](/documentation/PSReader/SearchConfiguration/resultTitleLabel)

Label configuration for the title line in search result cells (article headline, edition title).

[`resultSnippetLabel`](/documentation/PSReader/SearchConfiguration/resultSnippetLabel)

Label configuration for the snippet text in search result cells.

[`resultMetadataLabel`](/documentation/PSReader/SearchConfiguration/resultMetadataLabel)

Label configuration for the metadata line in search result cells (section name, page number).

[`editionDateFormatter`](/documentation/PSReader/SearchConfiguration/editionDateFormatter)

Formatter used to format edition dates in search result cells.

### Errors and Status Messages

[`errorTitleLabel`](/documentation/PSReader/SearchConfiguration/errorTitleLabel)

Label configuration for the primary error/status message title.

[`errorSubtitleLabel`](/documentation/PSReader/SearchConfiguration/errorSubtitleLabel)

Label configuration for the secondary error/status message subtitle.

