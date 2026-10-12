<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Choosing-an-Integration",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Choosing an Integration"
}
-->

# Choosing an Integration

Decide who builds your app’s reader experience: the SDK, with its prebuilt UI, or you, with a custom UI on the core SDK.

## Overview

The SDK has two sides. The **prebuilt UI** is a complete reader app that
you configure, brand, and connect to your services. A **custom UI** is
your own design, built on the core SDK: the engine the prebuilt UI runs
on, with the same page renderer.

Both sides work with every edition on PageSuite’s current system, classic
PDF editions included, so a custom UI for a classic PDF edition is fully
supported. “Feed” in API names such as [`FeedEditionService`](/documentation/PSReader/FeedEditionService) is the
current system’s old name, not a format. Editions on the legacy replica
system open only in the prebuilt UI. To check which system a title is on,
see
[Telling Which System a Publication Is On](/documentation/PSReader/Edition-Platforms#Telling-Which-System-a-Publication-Is-On).

|                                                                         |Prebuilt UI                                                                        |Custom UI                                                   |
|-------------------------------------------------------------------------|-----------------------------------------------------------------------------------|------------------------------------------------------------|
|You write                                                                |Configuration and delegates, plus your own navigation if you place screens yourself|Every screen: archive, reader chrome, page browser, settings|
|Archive, bookmarks, downloads, and search screens                        |Prebuilt                                                                           |Yours                                                       |
|Reader screen (navigation bar, content browser, loading screen, settings)|Prebuilt                                                                           |Yours, around the SDK’s page renderer                       |
|Features such as sharing, paywalls, and text-to-speech                   |Built in: you switch them on and connect delegates                                 |You build each one, from SDK parts where they exist         |
|Customization                                                            |Theming, configuration, delegates                                                  |Anything                                                    |
|Analytics                                                                |Ready-made events                                                                  |Your own, from the reader’s delegates                       |
|Classic PDF and responsive editions                                      |Yes                                                                                |Yes                                                         |
|Editions on the legacy replica system                                    |Yes                                                                                |No                                                          |

Choose the prebuilt UI when its screens, themed to your brand, fit your
app: it’s the least code, and features arrive as configuration. Choose a
custom UI when your design needs a reader screen of its own. The choice
isn’t all or nothing; see [Mixing Prebuilt and Custom UI](/documentation/PSReader/Choosing-an-Integration#Mixing-Prebuilt-and-Custom-UI).

## The Prebuilt UI

The prebuilt UI gives you archives, the reader screen, offline downloads,
bookmarks, search, and analytics events, all themed from one
[`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration). Delegates connect your paywall, sharing,
text-to-speech, commenting, adverts, and media. You can show it whole, or
place its screens one at a time in your own navigation.

**Whole, as the carousel.** [`CarouselViewController`](/documentation/PSReader/CarouselViewController) is a complete
reader app in one view controller. Give it a shortcode and it loads your
publications, their archives, and their reader settings from PageSuite:

```swift
let globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE"),
        .subsections("My Content", [
            .init(name: "Bookmarks", type: .bookmarks(type: .all)),
            .init(name: "Downloads", type: .downloads(type: .all))
        ])
    ]
)
```

See [Setting Up the Carousel](/documentation/PSReader/Setting-Up-the-Carousel).

**Screen by screen, in your own navigation.** Each screen the carousel
shows is also a view controller you can place yourself:
[`ArchiveViewController`](/documentation/PSReader/ArchiveViewController), [`BookmarksViewController`](/documentation/PSReader/BookmarksViewController),
[`DownloadsViewController`](/documentation/PSReader/DownloadsViewController), and [`SearchViewController`](/documentation/PSReader/SearchViewController).
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) opens one edition in the prebuilt reader
screen from anywhere, such as a button, a notification, or your own
archive list:

```swift
// An archive screen inside your own navigation.
let archive = ArchiveViewController(
    globalConfig: globalConfig,
    archiveType: .feedArchive(guid: "PUBLICATION_GUID", publicationName: "The Daily")
)
navigationController?.pushViewController(archive, animated: true)

// The latest edition, straight from a button.
let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

See [Embedding Prebuilt Screens](/documentation/PSReader/Embedding-Prebuilt-Screens) and
[Presenting the Prebuilt Reader](/documentation/PSReader/Presenting-the-Prebuilt-Reader). Every screen takes the same
configuration and delegates as the carousel, so you can start with one
and move to the other.

**What it costs:** the layout is the SDK’s. You can restyle and configure
every screen, but not rearrange it, and the reader screen is always the
SDK’s.

Editions on the legacy replica system open from the carousel and the
prebuilt screens, but not from [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController), which opens editions
on the current system only.

Continue with [Prebuilt UI](/documentation/PSReader/Prebuilt-UI).

## A Custom UI

A custom UI is built on the core SDK, the engine the prebuilt UI runs on.
You fetch the catalog with [`FeedEditionService`](/documentation/PSReader/FeedEditionService), open an edition, and
host [`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController), which renders pages and nothing
else, inside a screen you design:

```swift
import PSReader
import UIKit

final class LatestEditionViewController: UIViewController {

    private let reader = PSEditionReaderViewController()

    override func viewDidLoad() {
        super.viewDidLoad()

        // Host the reader as a child; your chrome goes around it.
        addChild(reader)
        reader.view.frame = view.bounds
        reader.view.autoresizingMask = [.flexibleWidth, .flexibleHeight]
        view.addSubview(reader.view)
        reader.didMove(toParent: self)

        Task {
            do {
                let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
                let published = try await service.latestEdition(publicationGUID: "PUBLICATION_GUID")
                let source = try await published.openEditionSource()
                reader.open(edition: source)
            } catch {
                // Show your own error state.
            }
        }
    }
}
```

**What you get:** full control. The archive, navigation bar, page
browser, loading screen, and settings are yours. The SDK reports the
state they need: paging through the reader’s delegates, download progress
through [`PSEDownloadObserver`](/documentation/PSReader/PSEDownloadObserver), and bookmark changes through
[`PSEBookmarkObserver`](/documentation/PSReader/PSEBookmarkObserver). [`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager) and [`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager)
handle offline reading and bookmarks.

**What it costs:** more code. There’s no configuration to theme,
because every pixel outside the pages is yours, and you build each
feature the prebuilt reader would have given you. Analytics come from the
reader’s delegates; of the prebuilt UI’s ready-made events, only
downloads and bookmarks still arrive.

Continue with [Custom UI](/documentation/PSReader/Custom-UI), which lists what you build and what the
SDK provides for each part. Moving from the legacy core SDK? Start with
[Migrating From the Legacy Core SDK](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK).

## Mixing Prebuilt and Custom UI

The two sides share one module and one model, so one app can use both:

- **Your archive, the prebuilt reader.** List editions with
  ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService`` in a design of your own, then open the one the
  user taps in the prebuilt reader:
  
  ```swift
  let reader = FeedReaderViewController(globalConfig: globalConfig, published: published)
  reader.modalPresentationStyle = .fullScreen
  present(reader, animated: true)
  ```
- **A custom UI with prebuilt parts.** Several prebuilt components take
  core models and work on their own:
  - **Sharing:** ``doc://com.pagesuite.PSReader/documentation/PSReader/WebReaderShareProvider`` and
    ``doc://com.pagesuite.PSReader/documentation/PSReader/ArticleLinkShareProvider`` build share content from a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage``
    and its edition. See <doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Share-Button>.
  - **Text-to-speech:** ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechProvider`` reads an article
    aloud from any listen button you add. See <doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Listen-Button>.
  - **Commenting:** ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider`` supplies the comment
    button, counts, and tooltips; forward the reader’s commenting delegate
    to it. See <doc://com.pagesuite.PSReader/documentation/PSReader/Adding-Comment-Buttons>.
  - **Search:** ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchService`` and its implementations are plain
    networking over public types. See <doc://com.pagesuite.PSReader/documentation/PSReader/Building-a-Search-Screen>.

[Building a Reader App](/documentation/PSReader/Building-a-Reader-App) shows both sides in one sample project, the
prebuilt reader opened from your own screen included.