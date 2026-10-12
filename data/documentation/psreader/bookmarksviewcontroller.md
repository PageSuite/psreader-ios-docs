<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/BookmarksViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)BookmarksViewController"
  },
  "title" : "BookmarksViewController"
}
-->

# BookmarksViewController

A standalone view controller for displaying bookmarked pages and articles.

```
@MainActor class BookmarksViewController
```

## Overview

The bookmarks view controller presents a customizable interface where users
can view and interact with their saved pages and articles from editions on
PageSuite’s current system and legacy replica editions. Users can open bookmarked items directly, remove
bookmarks, or manage their bookmark lists.

## Usage

```swift
let bookmarks = BookmarksViewController(
    globalConfig: globalConfig,
    type: .all
)

navigationController?.pushViewController(bookmarks, animated: true)
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Bookmarks>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksConfiguration``

## Topics

### Creating the Screen

[`init(globalConfig:bookmarksConfig:type:)`](/documentation/PSReader/BookmarksViewController/init(globalConfig:bookmarksConfig:type:))

Initializes a new standalone bookmarks view controller.

### Sorting

[`sortMode`](/documentation/PSReader/BookmarksViewController/sortMode-swift.property)

The current sort mode for displaying bookmarks.

[`BookmarksViewController.SortMode`](/documentation/PSReader/BookmarksViewController/SortMode-swift.enum)

Specifies the sort order for bookmarked content.

### Fitting the Screen Into Your Layout

[`additionalSafeAreaInsets`](/documentation/PSReader/BookmarksViewController/additionalSafeAreaInsets)

Extra insets the bookmarks grid keeps clear, on top of the safe area.

[`overrideUserInterfaceStyle`](/documentation/PSReader/BookmarksViewController/overrideUserInterfaceStyle)

Forces the bookmarks screen into light or dark mode.

