<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmark/editionSource(mode:among:onProgress:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader11PSEBookmarkO13editionSource4mode5among10onProgressAA010PSEEditionD0_p6source_AA7PSEPageCSg11openingPagetAA0B8OpenModeO_SayACGySfcSgtYaKF"
  },
  "title" : "editionSource(mode:among:onProgress:)"
}
-->

# editionSource(mode:among:onProgress:)

Resolves an edition source and opening page for this bookmark.

```
func editionSource(mode: PSEBookmarkOpenMode = .preferSourceEdition, among bookmarks: [PSEBookmark], onProgress: ((Float) -> Void)? = nil) async throws -> (source: PSEEditionSource, openingPage: PSEPage?)
```

## Parameters

`mode`

whether to prefer the bookmark’s own edition or always
use the bookmarks edition.

`bookmarks`

the set the bookmarks edition is built from, so a
fallback reader can page between siblings.

`onProgress`

streamed-edition download progress (0…1).

## Discussion

With [`PSEBookmarkOpenMode.preferSourceEdition`](/documentation/PSReader/PSEBookmarkOpenMode/preferSourceEdition) the bookmark’s own
edition is opened at the bookmarked page when available (downloaded,
or online), otherwise a bookmarks edition over `bookmarks` is
returned. [`PSEBookmarkOpenMode.alwaysBookmarksEdition`](/documentation/PSReader/PSEBookmarkOpenMode/alwaysBookmarksEdition) always
returns the bookmarks edition. Hand the result straight to
[`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:)).