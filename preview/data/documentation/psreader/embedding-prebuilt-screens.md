<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Embedding-Prebuilt-Screens",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Embedding Prebuilt Screens"
}
-->

# Embedding Prebuilt Screens

Place the prebuilt archive, bookmarks, downloads, and search screens in your own navigation.

## Overview

Every screen the carousel shows is also a view controller you can place
yourself. Each is a plain `UIViewController`: push it, put it in a tab,
or embed it in a screen of your own. Each one opens editions in the
prebuilt reader without any work from you.

```swift
import PSReader
import UIKit

let globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")

let archive = ArchiveViewController(
    globalConfig: globalConfig,
    archiveType: .feedArchive(guid: "PUBLICATION_GUID", publicationName: "The Daily")
)
archive.tabBarItem = UITabBarItem(title: "Editions", image: UIImage(systemName: "newspaper"), tag: 0)

let bookmarks = BookmarksViewController(globalConfig: globalConfig, type: .all)
bookmarks.tabBarItem = UITabBarItem(title: "Bookmarks", image: UIImage(systemName: "bookmark"), tag: 1)

let downloads = DownloadsViewController(globalConfig: globalConfig, downloadTypes: .all)
downloads.tabBarItem = UITabBarItem(title: "Downloads", image: UIImage(systemName: "arrow.down.circle"), tag: 2)

let tabBarController = UITabBarController()
tabBarController.viewControllers = [archive, bookmarks, downloads]
```

|View controller                                                                |Shows                                                 |More in                                                                            |
|-------------------------------------------------------------------------------|------------------------------------------------------|-----------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController``  |One publication’s editions, or a kiosk of publications|This guide                                                                         |
|``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksViewController``|The user’s bookmarked pages and articles              |<doc://com.pagesuite.PSReader/documentation/PSReader/Bookmarks>                    |
|``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsViewController``|Editions downloaded for offline reading               |<doc://com.pagesuite.PSReader/documentation/PSReader/Downloads-and-Offline-Reading>|
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchViewController``   |Search across your publications                       |<doc://com.pagesuite.PSReader/documentation/PSReader/Search>                       |

The screens take the same configurations and delegates as the carousel,
so one [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration) themes them all. To open an edition from your own
interface instead, such as a button or a list you design, use
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController); see [Presenting the Prebuilt Reader](/documentation/PSReader/Presenting-the-Prebuilt-Reader).
To show every screen at once, in the SDK’s own tabs, see
[Setting Up the Carousel](/documentation/PSReader/Setting-Up-the-Carousel).

## Embedding a Screen

UIKit apps place the screens like any other view controller. In SwiftUI,
wrap one in a `UIViewControllerRepresentable`; its coordinator is a good
home for delegates that need your app’s state, such as a paywall that
checks the user’s subscription:

**UIKit:**

```swift
let archive = ArchiveViewController(
    globalConfig: globalConfig,
    archiveType: .feedArchive(guid: "PUBLICATION_GUID", publicationName: "The Daily")
)
navigationController?.pushViewController(archive, animated: true)
```

Each screen fills its view, and your navigation bar and tab bar
stay yours.

**SwiftUI:**

```swift
import PSReader
import SwiftUI

struct ArchiveView: UIViewControllerRepresentable {
    let isSubscribed: Bool

    func makeCoordinator() -> Coordinator {
        Coordinator()
    }

    func makeUIViewController(context: Context) -> ArchiveViewController {
        context.coordinator.isSubscribed = isSubscribed

        let globalConfig = GlobalConfiguration(
            apiKey: "API_KEY",
            accountGUID: "ACCOUNT_GUID",
            paywallDelegate: context.coordinator
        )
        return ArchiveViewController(
            globalConfig: globalConfig,
            archiveType: .feedArchive(guid: "PUBLICATION_GUID", publicationName: "The Daily")
        )
    }

    func updateUIViewController(_ archive: ArchiveViewController, context: Context) {
        context.coordinator.isSubscribed = isSubscribed
    }

    final class Coordinator: PaywallDelegate {
        var isSubscribed = false

        func paywallViewControllerForAction(openFeedEdition published: PSEPublished) -> PaywallViewController? {
            isSubscribed ? nil : SubscribeViewController()
        }

        func paywallViewControllerForAction(openReplicaEdition edition: PSEdition) -> PaywallViewController? {
            nil
        }
    }
}
```

`SubscribeViewController` stands for your own paywall screen; see
[Paywalls](/documentation/PSReader/Paywalls). The same pattern works for any delegate: conform
the coordinator and pass `context.coordinator` to the matching
[`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration) parameter.

## Setting the App Configuration

Screens you embed have no dynamic archive to load your app configuration
from PageSuite, and a few reader features read it, in-article adverts
among them. If your editions use them, load the configuration with
[`AppConfigService`](/documentation/PSReader/AppConfigService) and set it on your global configuration before you
create the screens, which copy the global configuration when you create
them:

```swift
var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
globalConfig.remoteConfig = try? await AppConfigService().configuration(forShortcode: "SHORTCODE")

let archive = ArchiveViewController(
    globalConfig: globalConfig,
    archiveType: .feedArchive(guid: "PUBLICATION_GUID", publicationName: "The Daily")
)
```

Run it in an async context, such as a `Task` you start when your scene
connects, and create the screens once it returns.
[The App Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration) lists the
features that need it; if your editions use none of them, skip this step.

## Showing an Archive

[`ArchiveViewController`](/documentation/PSReader/ArchiveViewController) shows one publication’s editions in a grid, the
latest edition first and largest. Create it with the publication GUID and
a publication name, which becomes each edition’s
[`publicationName`](/documentation/PSReader/PSEPublished/publicationName):

```swift
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.maxContentWidth = 900
archiveConfig.datePicker = ArchiveDatePickerConfiguration(globalConfig: globalConfig)

let archive = ArchiveViewController(
    globalConfig: globalConfig,
    archiveConfig: archiveConfig,
    archiveType: .feedArchive(guid: "PUBLICATION_GUID", publicationName: "The Daily")
)
```

[`ArchiveConfiguration`](/documentation/PSReader/ArchiveConfiguration) controls the grid: thumbnail shape
([`cellAspectRatio`](/documentation/PSReader/ArchiveConfiguration/cellAspectRatio) and
[`thumbnailContentMode`](/documentation/PSReader/ArchiveConfiguration/thumbnailContentMode)), labels, the download
button, how many editions to list, and the reader that editions open in.
Two values matter most when you embed the screen:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/maxContentWidth`` caps the grid’s width in a
  regular-width environment, such as a full-screen iPad, and centers it.
  Compact widths ignore it.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/datePicker`` adds a month picker above the grid.
  The editions for a month come from the backend that
  ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/feedPublicationType-swift.property`` names, which must match the
  publication’s type in PageSuite. The default, `.app`, suits most
  publications; ask PageSuite if you’re unsure.

> Replica: `.replicaArchive(guid:)` shows a publication on the legacy
> replica system, from its replica publication GUID. The archive lists the
> latest 30 editions unless you set ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/archiveLimit``.

## Showing a Kiosk

A kiosk is a grid of publications, each shown by its cover.
Tapping one opens that publication’s archive: pushed onto your navigation
controller if the kiosk is in one, presented otherwise.

```swift
let kiosk = ArchiveViewController(
    globalConfig: globalConfig,
    archiveType: .feedPublicationKiosk(publications: [
        KioskFeedPublication(name: "The Daily", guid: "PUBLICATION_GUID"),
        KioskFeedPublication(name: "The Weekend", guid: "WEEKEND_PUBLICATION_GUID"),
        KioskFeedPublication(name: "The Magazine", guid: "MAGAZINE_PUBLICATION_GUID", archiveConfig: magazineConfig)
    ])
)
```

![A kiosk grid on iPad showing the latest cover of each publication.](images/com.pagesuite.PSReader/kiosk-grid-ipad@2x.png)

The kiosk’s own configuration styles the grid, and each publication’s
archive uses it too, unless the [`KioskFeedPublication`](/documentation/PSReader/KioskFeedPublication) carries an
[`archiveConfig`](/documentation/PSReader/KioskFeedPublication/archiveConfig) of its own.

> Replica: `.replicaPublicationKiosk(publications:)` is a kiosk of
> legacy replica publications, each a ``doc://com.pagesuite.PSReader/documentation/PSReader/KioskReplicaPublication`` created
> from its replica publication GUID. A kiosk can’t mix them with
> publications on the current system.

## Showing Bookmarks and Downloads

[`BookmarksViewController`](/documentation/PSReader/BookmarksViewController) lists the pages and articles the user has
bookmarked, and [`DownloadsViewController`](/documentation/PSReader/DownloadsViewController) the editions they’ve saved
for offline reading. Both filter by kind:

```swift
let bookmarks = BookmarksViewController(
    globalConfig: globalConfig,
    type: [.feedPage, .feedArticle]
)
bookmarks.sortMode = .byDate

let downloads = DownloadsViewController(
    globalConfig: globalConfig,
    downloadTypes: .feedEdition
)
```

In the carousel, a section whose first screen is bookmarks or downloads
has a menu in its ribbon that sorts these lists. On their own, the
screens have no menu, so let users change the order with a control of
your own that sets `sortMode`. Each screen remembers the order
across launches. The feature guides cover the rest, a sort button
included: [Bookmarks](/documentation/PSReader/Bookmarks) and [Downloads and Offline Reading](/documentation/PSReader/Downloads-and-Offline-Reading).

## Showing Search

[`SearchViewController`](/documentation/PSReader/SearchViewController) searches a set of publications that a
[`SearchDelegate`](/documentation/PSReader/SearchDelegate) supplies. [`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate) supplies the
publications a shortcode names. Pass `dismissible: true` when you present
the screen, so it shows a close button:

```swift
let searchDelegate = ApplicationSearchDelegate(
    shortcode: "SHORTCODE",
    readerConfig: ReaderConfiguration(globalConfig: globalConfig)
)

let search = SearchViewController(
    globalConfig: globalConfig,
    delegate: searchDelegate,
    dismissible: true
)
present(search, animated: true)
```

[Search](/documentation/PSReader/Search) covers the prebuilt search in full, including search
inside the reader. To design the search screen yourself, see
[Building a Search Screen](/documentation/PSReader/Building-a-Search-Screen).

## Choosing the Reader They Open

Each screen opens editions in a reader set up by its own configuration’s
`readerConfig`. To make every screen open the same reader, with the same
settings rows, for example, build one [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) and assign
it to each configuration. [Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI) shows how, and
[Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen) covers what the reader configuration
controls.

## Fitting Screens Into Your Layout

When something of yours covers part of a screen, such as a mini player
along the bottom, add the space to the screen’s
`additionalSafeAreaInsets` so its content stays clear:

```swift
archive.additionalSafeAreaInsets = UIEdgeInsets(top: 0, left: 0, bottom: 64, right: 0)
```

The bookmarks and downloads screens re-lay out their grids when you set
it, and apply it even inside a SwiftUI paging `TabView`, where UIKit alone
doesn’t.

To force a screen into light or dark mode, set its
`overrideUserInterfaceStyle`; the bookmarks, downloads, and search screens
pass it on to everything they embed. To force one style everywhere, the
readers your screens open included, set it on your app’s window instead.
See [Dark Mode](/documentation/PSReader/Theming#Dark-Mode).

## Topics

### Archive Screens

[`ArchiveViewController`](/documentation/PSReader/ArchiveViewController)

A standalone view controller for displaying publication archives.

[`ArchiveConfiguration`](/documentation/PSReader/ArchiveConfiguration)

Configuration for customizing the appearance and behavior of publication archive views.

[`ArchiveDatePickerConfiguration`](/documentation/PSReader/ArchiveDatePickerConfiguration)

Configuration object for customizing the appearance and behavior of the
archive date picker within the SDK.

### Kiosks

[`KioskFeedPublication`](/documentation/PSReader/KioskFeedPublication)

Describes an entry in a kiosk grid of publications on PageSuite’s current
system.

[`KioskReplicaPublication`](/documentation/PSReader/KioskReplicaPublication)

Describes a replica publication entry in a kiosk grid.

