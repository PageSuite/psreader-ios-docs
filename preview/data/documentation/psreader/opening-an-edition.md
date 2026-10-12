<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Opening-an-Edition",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Opening an Edition"
}
-->

# Opening an Edition

Turn a catalog entry into an edition source that your reader screen can show.

## Overview

The reader opens a [`PSEEditionSource`](/documentation/PSReader/PSEEditionSource): the loaded [`PSEEdition`](/documentation/PSReader/PSEEdition) plus
the machinery that delivers its page assets. One call covers almost every
case, [`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)):

```swift
let source = try await published.openEditionSource { progress in
    progressView.setProgress(progress, animated: true)   // 0…1 while the opening pages download
}

reader.open(edition: source)
```

Your reader screen, `ReaderScreenViewController` from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader), makes this call itself when you create it with
`init(published:openingPageGUID:)`. To show a source you opened another
way, such as those in the sections below, create it with
`init(source:openingPage:)`. Using the prebuilt UI?
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) opens editions for you; see
[Presenting the Prebuilt Reader](/documentation/PSReader/Presenting-the-Prebuilt-Reader).

The reader renders classic PDF pages and responsive pages alike, including
editions that mix the two, so the same source and the same reader work for
every publication on PageSuite’s current edition system.

[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) picks the best backing for
the edition’s current state:

1. A completed download opens as a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadedEdition``, fully offline.
1. Anything else opens as a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEStreamingEdition``, which fetches page
   assets over the network as the user reads.

A download carried over from the legacy SDK, whose
[`isBridged`](/documentation/PSReader/PSEPublished/isBridged) is `true`, is the exception: this call can’t
open it, so open it with [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition) instead; see
[Opening Migrated Editions](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#Opening-Migrated-Editions).

To gate the attempt, check [`isAvailableToOpen`](/documentation/PSReader/PSEPublished/isAvailableToOpen) first. It’s
`true` when a downloaded copy exists or the device is online.

## Driving a Loading UI

Opening is asynchronous, so put whatever loading treatment fits your app
between the tap and the reader: a cover splash, a skeleton, or a plain
spinner. The reader screen in [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader) shows a spinner
until progress arrives, then a progress bar; replace them with your own.
The SDK supplies the signals, not the screen:

- **Progress.** A streamed edition downloads a small set of opening assets
  before the source returns, and `onProgress` reports that download from 0
  to 1 on the main queue. A downloaded edition opens without reporting
  progress, so treat progress as optional.
- **Cover, name, and date.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/image``, the cover’s URL, is
  available before anything opens, so a splash can show the cover at once,
  with the edition’s `name` and date. Show ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/editionDate``,
  falling back to ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/datePublished``, or the name alone when
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/useCustomEditionName`` is `true`.
- **Errors and retry.** The call throws when the edition can’t be opened,
  for example offline with no download, or on a backend error. Show your
  failure state, and retry by calling
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)`` again; a failed open
  leaves nothing to clean up.

## Choosing the Opening Page

The reader starts at the front of the edition unless you pass an opening
page. Your reader screen takes the page’s GUID and looks it up once the
edition opens:

```swift
let screen = ReaderScreenViewController(published: published, openingPageGUID: "PAGE_GUID")
```

With a source you’ve opened, look the page up yourself with
[`page(forGUID:)`](/documentation/PSReader/PSEEdition/page(forGUID:)):

```swift
let page = source.edition.page(forGUID: "PAGE_GUID")
let screen = ReaderScreenViewController(source: source, openingPage: page)
```

An unknown GUID finds no page, and the reader then opens at the front.

### Resuming Where the User Left Off

Your reader screen runs `updateChrome()` each time the reader settles on a
page, including the page it opens on. Save the page there, keyed by the
edition’s [`publishedGUID`](/documentation/PSReader/PSEPublished/publishedGUID), and remember the edition and
page for a “Continue reading” button. In `updateChrome()`, add:

```swift
// Remember where the user is in this edition, for next time.
UserDefaults.standard.set(page.pageguid, forKey: "lastPage-\(published.publishedGUID)")

// And the last edition read, with its page, for "Continue reading".
UserDefaults.standard.set(published.editionGUID, forKey: "lastEditionGUID")
UserDefaults.standard.set(page.pageguid, forKey: "lastEditionPageGUID")
```

When you open the edition again, pass the saved page’s GUID:

```swift
let lastPageGUID = UserDefaults.standard.string(forKey: "lastPage-\(published.publishedGUID)")
let screen = ReaderScreenViewController(published: published, openingPageGUID: lastPageGUID)
```

Saving as the edition opens doesn’t replace the saved page with the
front page. [`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:))
settles the reader on the opening page before it returns, so the first
`updateChrome()` saves the page the reader opened on;
[`currentPage()`](/documentation/PSReader/PSEditionReaderViewController/currentPage()) is `nil` only before an
edition is open.

For “Continue reading”, resolve the saved edition, as
[Opening From an Edition GUID](/documentation/PSReader/Opening-an-Edition#Opening-From-an-Edition-GUID) shows, and open it on the saved page:

```swift
guard let editionGUID = UserDefaults.standard.string(forKey: "lastEditionGUID") else {
    return
}

let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
let published = try await service.published(forEditionGUID: editionGUID)

let screen = ReaderScreenViewController(
    published: published,
    openingPageGUID: UserDefaults.standard.string(forKey: "lastEditionPageGUID")
)
```

The button keeps its own copy of the page because the entry the lookup
returns may not be the one the user read. For an edition published once,
it’s the catalog’s entry, with the same `publishedGUID`. An edition
published more than once has a catalog entry for each publish, each with
its own `publishedGUID`, and the lookup returns one of them, so a page
saved under another entry’s `publishedGUID` wouldn’t be found.

Refresh the button in `viewWillAppear(_:)` of the screen that shows it.
Your reader screen is presented full screen, so that runs again when the
user closes it. Store page GUIDs rather than indexes: a GUID names the
same page in single- and double-page mode, and a spread index doesn’t.

## Opening From an Edition GUID

Search results and deep links often carry only an edition GUID.
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)) resolves it to a catalog
entry, including editions older than the catalog returns, ready to open:

```swift
let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
let published = try await service.published(forEditionGUID: "EDITION_GUID")

let screen = ReaderScreenViewController(published: published, openingPageGUID: pageGUID)
```

The entry carries less than one from the catalog: its
[`publicationName`](/documentation/PSReader/PSEPublished/publicationName) and [`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID) are
empty. So your reader screen shows the edition’s name as its title, and
code that needs the publication GUID uses the one you already hold. If you
know the publication’s name, set `publicationName` on the entry before you
create the screen, as the routing below does.

### Routing Links and Notifications

The payload and URL formats are your own: put the edition GUID in them,
the publication GUID so the screen can name the publication, and a page
GUID when you want a specific page. This scene delegate reads a link such
as `yourapp://edition/EDITION_GUID?publication=PUBLICATION_GUID&page=PAGE_GUID`
and presents your reader screen:

```swift
/// Your publications' names, by publication GUID: the names you pass
/// when you load their catalogs.
let publicationNames = ["PUBLICATION_GUID": "The Daily"]

func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    guard let url = URLContexts.first?.url,
          url.scheme == "yourapp",
          url.host == "edition",
          let editionGUID = url.pathComponents.dropFirst().first else { return }

    let queryItems = URLComponents(url: url, resolvingAgainstBaseURL: false)?.queryItems ?? []
    let publicationGUID = queryItems.first(where: { $0.name == "publication" })?.value
    let pageGUID = queryItems.first(where: { $0.name == "page" })?.value

    openEdition(editionGUID: editionGUID, publicationGUID: publicationGUID, pageGUID: pageGUID)
}

func openEdition(editionGUID: String, publicationGUID: String?, pageGUID: String?) {
    Task {
        do {
            let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
            let published = try await service.published(forEditionGUID: editionGUID)

            // The lookup leaves the publication's name empty; the screen
            // shows it as its title.
            if let publicationGUID, let name = publicationNames[publicationGUID] {
                published.publicationName = name
            }

            let screen = ReaderScreenViewController(published: published, openingPageGUID: pageGUID)
            let navigationController = UINavigationController(rootViewController: screen)
            navigationController.modalPresentationStyle = .fullScreen
            window?.rootViewController?.present(navigationController, animated: true)
        } catch {
            window?.rootViewController?.showAlert(title: "Couldn't Open Edition", error: error)
        }
    }
}
```

A link that launches your app arrives in `scene(_:willConnectTo:options:)`
instead. Once the window is set up there, pass it on with
`self.scene(scene, openURLContexts: connectionOptions.urlContexts)`. A push
notification arrives in your `UNUserNotificationCenter` delegate’s
`userNotificationCenter(_:didReceive:withCompletionHandler:)`; read the
GUIDs from its payload and call the same method.
`showAlert(title:error:retry:)` comes from [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader).

### When You Only Have a Page Label

Send page GUIDs where you can: a GUID names exactly one page, while a
printed label such as “A3” is free text from the publisher. If all you
have is a label, open the edition first, look the page up by
[`pageLabel`](/documentation/PSReader/PSEPage/pageLabel), and create the reader screen with the source and
the page:

```swift
let source = try await published.openEditionSource()
let page = source.edition.pages?.first { $0.pageLabel == "A3" }

let screen = ReaderScreenViewController(source: source, openingPage: page)
```

Labels can repeat within an edition, so this opens the first match.

## Opening While Downloading

To make “download and read” feel instant, don’t wait for the whole
download. Start it, and open the edition as soon as its
[`PSEDownloadManager.DownloadPhase.splash`](/documentation/PSReader/PSEDownloadManager/DownloadPhase/splash) phase completes. The
[`PSEDownloadManager.DownloadPhase.main`](/documentation/PSReader/PSEDownloadManager/DownloadPhase/main) phase keeps filling the download
while the user reads:

```swift
extension EditionListViewController: PSEDownloadObserver {

    func downloadAndOpen(_ published: PSEPublished) {
        let manager = PSEDownloadManager.shared
        let state = manager.addObserver(self, published: published)
        manager.downloadImmediately(published: published)

        // The edition may already be far enough along.
        downloadManager(manager, downloadFor: published, didChangeState: state)
    }

    func downloadManager(_ manager: PSEDownloadManager,
                         downloadFor published: PSEPublished,
                         didChangeState state: PSEDownloadManager.DownloadState) {
        switch state {
        case .downloading(phase: .main, _, _), .downloaded:
            manager.removeObserver(self)
            Task {
                do {
                    let source = try await PSEDownloadedEdition.open(published: published)
                    let screen = ReaderScreenViewController(source: source)
                    present(UINavigationController(rootViewController: screen), animated: true)
                } catch {
                    showAlert(title: "Couldn't Open Edition", error: error)
                }
            }
        default:
            break
        }
    }
}
```

The download manager holds observers weakly, so the observer must outlive
the download; an archive screen that stays on screen works. See
[Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button) for the rest of the download API.

## Choosing a Source Explicitly

Each source can also be opened directly when you want to bypass the
automatic choice, for example to offer “read online” even when a download
exists:

```swift
let streamed = try await PSEStreamingEdition.open(published: published)
let downloaded = try await PSEDownloadedEdition.open(published: published)

let screen = ReaderScreenViewController(source: streamed)
```

[`open(published:)`](/documentation/PSReader/PSEDownloadedEdition/open(published:)) throws when the edition hasn’t
been downloaded, or is still queued.

[`PSEBookmarksEdition`](/documentation/PSReader/PSEBookmarksEdition) is different: it isn’t opened from a catalog entry
but built from saved bookmarks, one page per bookmark, and reads offline.
See [Opening a Bookmark](/documentation/PSReader/Adding-a-Bookmark-Button#Opening-a-Bookmark).

## Custom Sources

Conform to [`PSEEditionSource`](/documentation/PSReader/PSEEditionSource) yourself only to feed the reader from a
system the SDK doesn’t know about. A minimal conformance supplies
`published` and `edition`; the protocol’s other requirements have
defaults:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEditionSource/resourceManager``, a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEditionResourceManager``,
  resolves resource references to files, URLs, or data. The default reads
  the edition’s cache directory and fetches absolute URLs over HTTP.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEditionSource/pageSource``, a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPageSpreadSource``, reports each
  spread’s asset availability so the reader can show loading and retry
  states. The default, `nil`, treats every asset as available.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEditionSource/pagePrefetching``, a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPageSpreadPrefetching``,
  lets the source warm upcoming pages as the user reads. The default,
  `nil`, prefetches nothing.

## Topics

### Edition Sources

[`PSEEditionSource`](/documentation/PSReader/PSEEditionSource)

A reader-ready edition: the loaded content plus the machinery that
delivers its page assets.

[`PSEStreamingEdition`](/documentation/PSReader/PSEStreamingEdition)

An edition source that streams page assets from the network as the user
reads.

[`PSEDownloadedEdition`](/documentation/PSReader/PSEDownloadedEdition)

An edition source backed by a copy stored on device by
[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager).

[`PSEBookmarksEdition`](/documentation/PSReader/PSEBookmarksEdition)

An edition source synthesized from saved bookmarks: one page per
bookmark, readable offline.

[`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition)

An edition source that opens an edition saved with the legacy SDK in the
current reader.

### Custom Sources

[`PSEEditionResourceManager`](/documentation/PSReader/PSEEditionResourceManager)

Resolves an edition’s resource references (page PDFs, images, templates)
to concrete locations or data.

[`PSEDataTask`](/documentation/PSReader/PSEDataTask)

A cancellable in-flight resource fetch, as returned by
[`dataTask(for:completion:)`](/documentation/PSReader/PSEEditionResourceManager/dataTask(for:completion:)).

[`PSEPageSpreadSource`](/documentation/PSReader/PSEPageSpreadSource)

Exposes per-spread asset availability for editions whose pages arrive
asynchronously.

[`PSEPageSpreadObserver`](/documentation/PSReader/PSEPageSpreadObserver)

Receives per-spread download state changes from a [`PSEPageSpreadSource`](/documentation/PSReader/PSEPageSpreadSource).

[`PSEPageSpreadState`](/documentation/PSReader/PSEPageSpreadState)

The download state of one page spread’s assets.

[`PSEPageSpreadPrefetching`](/documentation/PSReader/PSEPageSpreadPrefetching)

Lets an edition source warm upcoming page assets as the user reads.

[`PSEPageSpreadPrefetchDirection`](/documentation/PSReader/PSEPageSpreadPrefetchDirection)

The reading direction driving a prefetch request.

