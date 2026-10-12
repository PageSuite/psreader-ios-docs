<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/BookmarksConfiguration",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22BookmarksConfigurationV"
  },
  "title" : "BookmarksConfiguration"
}
-->

# BookmarksConfiguration

Configuration for customizing the appearance and behavior of bookmark archives.

```
struct BookmarksConfiguration
```

## Overview

The bookmarks archive allows users to easily access bookmarked pages and articles
across editions on PageSuite’s current system and legacy replica editions. This view presents thumbnails,
headlines, publication information, and dates for bookmarked content in a grid layout.

Use this configuration to align the bookmarks view with your application’s design,
including typography, colors, layout, and placeholder imagery.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Bookmarks>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksViewController``

## Topics

### Creating a Configuration

[`init(globalConfig:)`](/documentation/PSReader/BookmarksConfiguration/init(globalConfig:))

Initializes a new bookmarks configuration using defaults from the provided global SDK configuration.

### Choosing Bookmarks

[`BookmarksConfiguration.BookmarkType`](/documentation/PSReader/BookmarksConfiguration/BookmarkType)

An option set representing the types of bookmarks supported by the bookmarks view.

### Appearance

[`backgroundColor`](/documentation/PSReader/BookmarksConfiguration/backgroundColor)

Background color of the bookmarks view.

[`placeholderColor`](/documentation/PSReader/BookmarksConfiguration/placeholderColor)

Placeholder color shown during loading states within the bookmarks view.

[`assetDelegate`](/documentation/PSReader/BookmarksConfiguration/assetDelegate)

Delegate providing custom images used within the bookmarks view.

### Thumbnails

[`aspectRatio`](/documentation/PSReader/BookmarksConfiguration/aspectRatio)

Aspect ratio applied to bookmark thumbnails displayed within the view.

[`thumbnailContentMode`](/documentation/PSReader/BookmarksConfiguration/thumbnailContentMode)

Content mode determining how bookmark thumbnails scale and fit within their containers.

### Rows

[`publicationLabel`](/documentation/PSReader/BookmarksConfiguration/publicationLabel)

Label configuration for displaying the publication name associated with a bookmark.

[`headlineLabel`](/documentation/PSReader/BookmarksConfiguration/headlineLabel)

Label configuration for displaying article headlines associated with bookmarks.

[`pageLabel`](/documentation/PSReader/BookmarksConfiguration/pageLabel)

Label configuration for displaying the page information (e.g., “Page 1”) associated with a bookmark.

[`dateLabel`](/documentation/PSReader/BookmarksConfiguration/dateLabel)

Label configuration for displaying bookmark dates.

[`dateFormatter`](/documentation/PSReader/BookmarksConfiguration/dateFormatter)

Formatter used for generating date strings displayed in bookmark listings.

[`bookmarkedIconColor`](/documentation/PSReader/BookmarksConfiguration/bookmarkedIconColor)

Tint color for the bookmark icon indicating bookmarked items.

[`rowDividerColor`](/documentation/PSReader/BookmarksConfiguration/rowDividerColor)

Color of the divider line displayed between bookmark rows.

### Empty State

[`noContentConfig`](/documentation/PSReader/BookmarksConfiguration/noContentConfig)

Configuration for displaying the no bookmarks available state.

### Opening Bookmarks

[`readerConfig`](/documentation/PSReader/BookmarksConfiguration/readerConfig)

Reader configuration applied when opening bookmarked content.

