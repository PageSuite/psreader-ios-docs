<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Migrating-From-PSReaderUI",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Migrating From PSReaderUI"
}
-->

# Migrating From PSReaderUI

Move an app built on the PSReaderUI SDK to the unified PSReader SDK: change the import, then the few APIs that changed.

## Overview

The prebuilt UI you know as PSReaderUI is now part of the `PSReader`
module, together with the core SDK it’s built on. Its screens,
configurations, and delegates keep their names. Start with the import:

```swift
// Before
import PSReaderUI

// After
import PSReader
```

Then work through the sections below. Each names the API it affects, so
skip any your app doesn’t use. The change log’s [v26.8.0](/documentation/PSReader/Change-Log#v2680)
entry lists the release’s other changes.

## The Module

- **Imports.** Replace every `import PSReaderUI` with `import PSReader`.
  A file that imported both needs only `import PSReader`.
- **Module-qualified names.** `PSReaderUI.CarouselViewController` becomes
  `PSReader.CarouselViewController`, or plain `CarouselViewController`.
  The PSReaderUI docs qualified most names, so search your project for
  `PSReaderUI.`. `PSReader.initialize(apiKey:completion:)` is unchanged.
- **Frameworks.** One `PSReader.xcframework` replaces
  `PSReaderUI.xcframework` and `PSReader.xcframework`. The Apryse
  frameworks, `PDFNet.xcframework` and `Tools.xcframework`, stay.
- **Swift Package Manager and CocoaPods.** Nothing moves: the same
  package and `PSReaderSDK` product, and the same `PSReaderUI2` pod. Update
  to 26.8.0.

## The Edition Launch Event

[`EventChannel.AnalyticsEvent.feedEditionLaunch(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionLaunch(_:)) now carries an
[`EventChannel.FeedEditionEventContext`](/documentation/PSReader/EventChannel/FeedEditionEventContext), like the other `feedEdition…`
events, in place of the `PSEPublished`. Read the edition from the
context:

```swift
func analytics(event: EventChannel.AnalyticsEvent) {
    switch event {
    // Before: case .feedEditionLaunch(let published):
    case .feedEditionLaunch(let context):
        guard let published = context.published else { return }
        print("Opened", published.name)
    default:
        break
    }
}
```

## Icons and Strings the SDK No Longer Requests

These cases are gone. Delete any `switch` arms that name them, in your
asset delegate or your [`LocalizationManager`](/documentation/PSReader/LocalizationManager) subclass, and their entries
in your translations:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageResourceName``: `backToSectionStart`, `clear`, and `print`.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/LegacyImageResourceName``: `back` and `search`.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey``: `changeDate`, `downloadingImages`,
  `editionPrintJob`, `noRecentViewedEditionsTitle`,
  `noRecentViewedEditionsMessage`, and `offlineMessage`.

One key is new: [`LocalizedStringKey.searchMinimumCharacters`](/documentation/PSReader/LocalizedStringKey/searchMinimumCharacters), the
message search shows for a query under three characters. Add it to your
translations; see [Localization](/documentation/PSReader/Localization).

## The Version Globals

`PSReaderUIVersionNumber` and `PSReaderUIVersionString` are gone with
the module. Use `PSReaderVersionNumber` and `PSReaderVersionString`.

## The Core SDK’s Types

The models the prebuilt delegates hand you, such as `PSEPublished`,
`PSEPage`, `PSEArticle`, and `PSEdition`, keep their names. These changes
matter only if your app used the core module’s managers or reader
directly:

|Before                                                      |Now                                                                                                                               |
|------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
|`PSELocalBookmarkManager`                                   |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager``                                                        |
|`PSEDownloadManager.getDownloaded(publishedGUID:)`          |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/downloadedEdition(for:)``, which takes the `PSEPublished`|
|`PSEDownloadManager.deleteDownloadedEditonsIfModified(for:)`|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/removeOutdatedDownload(for:)``                           |
|`PSEDownloadManager.ToggleDownloadStatus.canceled`          |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/ToggleDownloadStatus/cancelled``                         |
|`PSEditionReaderViewController.reload()`                    |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/reloadData()``                                |
|`PSEditionReaderViewController.reloadPages()`               |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/reloadPageContent()``                         |
|`PSEAdvertDelegate`                                         |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol``               |
|`ScrollCollapseController`                                  |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEScrollCollapseController``                                               |

[`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager) is `PSELocalBookmarkManager` renamed; the legacy
class that used the name before, created with
`init(application:cookieDelegate:)`, is gone. Its methods are renamed
too: adding and toggling now throw, a toggle returns a
[`PSEBookmarkChange`](/documentation/PSReader/PSEBookmarkChange) in place of a tuple, and `application:` is
optional.

|`PSELocalBookmarkManager`                                               |`PSEBookmarkManager`                                                                                                                   |
|------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|`bookmark(page:inEdition:inPublished:inApplication:)`                   |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/addBookmark(forPage:edition:published:application:)``         |
|`bookmark(article:inPage:inEdition:inPublished:inApplication:)`         |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/addBookmark(forArticle:in:edition:published:application:)``   |
|`toggleBookmark(page:inEdition:inPublished:inApplication:)`             |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forPage:edition:published:application:)``      |
|`toggleBookmark(forArticle:inPage:inEdition:inPublished:inApplication:)`|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:)``|
|`toggleBookmark(context:inEdition:inPublished:inApplication:)`          |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/toggleBookmark(context:edition:published:application:)``      |
|`deleteBookmarked(page:)`                                               |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeBookmark(forPage:)``                                    |
|`deleteBookmarked(article:page:)`                                       |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeBookmark(forArticle:page:)``                            |
|`deleteBookmark(_:)`, `deleteBookmark(_:page:)`                         |`removeBookmark(_:)`, `removeBookmark(_:page:)`                                                                                        |
|`deleteBookmarks()`                                                     |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeAllBookmarks()``                                        |
|`hasBookmarks()`                                                        |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/hasBookmarks``                                                |

## What’s New for a Prebuilt App

- **Your own lists.** ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService`` fetches a publication’s
  editions, its latest edition, or a range of dates, for your own list or
  button that opens the prebuilt reader. See
  <doc://com.pagesuite.PSReader/documentation/PSReader/Fetching-the-Archive> and
  <doc://com.pagesuite.PSReader/documentation/PSReader/Presenting-the-Prebuilt-Reader#Opening-an-Edition-You-Fetched>.
- **The app configuration.** ``doc://com.pagesuite.PSReader/documentation/PSReader/AppConfigService`` loads a shortcode’s
  configuration for screens you embed and readers you open yourself.
- **Settings rows.** ``doc://com.pagesuite.PSReader/documentation/PSReader/SettingsConfiguration/additionalItems`` adds rows
  of your own to the reader’s settings menu. See
  <doc://com.pagesuite.PSReader/documentation/PSReader/Customizing-the-Reader-Screen#Adding-Your-Own-Rows>.
- **Layout.** ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/maxContentWidth`` caps an archive’s
  width on wide screens, and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/setRibbonLayout(section:subsectionAlignment:)``
  changes the carousel’s ribbons after it’s created.
- **Fewer stubs.** The replica methods of ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertDelegate``,
  ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate``, ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareDelegate``, ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioSessionProvider``, and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechArticleFormatter`` now have default implementations, so a
  feed-only app can delete its replica stubs.
- **A custom UI.** The core SDK is documented for building your own
  reader screens, alone or beside the prebuilt ones. See
  <doc://com.pagesuite.PSReader/documentation/PSReader/Choosing-an-Integration> and <doc://com.pagesuite.PSReader/documentation/PSReader/Custom-UI>.
- **Agents and a sample.** <doc://com.pagesuite.PSReader/documentation/PSReader/Using-the-SDK-With-AI-Agents> points a
  coding agent at these docs, and <doc://com.pagesuite.PSReader/documentation/PSReader/Building-a-Reader-App> walks
  through a sample project for both sides.