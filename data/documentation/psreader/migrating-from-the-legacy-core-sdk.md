<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Migrating From the Legacy Core SDK"
}
-->

# Migrating From the Legacy Core SDK

Move an app from the legacy PSReader Core SDK to the current SDK, and keep
what its users saved.

## Overview

The current SDK replaces the legacy Core SDK rather than extending it, and
two migrations happen together:

- **Backend.** The legacy SDK read the legacy replica system. The current
  SDK reads editions from PageSuite’s current system, which serves
  classic PDF editions as well as responsive ones. Your
  publications must be set up on the current system before the app
  migration ships; your account manager coordinates this. Each
  publication gets a new publication GUID there, distinct from its replica
  publication GUID, so ask for the mapping.
- **App code.** No legacy call site compiles unchanged. How much you
  rewrite depends on the side you move to: the prebuilt UI replaces your
  screens, and a custom UI keeps them and ports each mechanism.

The legacy `PS`-prefixed classes this guide maps, such as
`PSReaderViewController`, remain inside the module for compatibility;
most other legacy types are gone. They’re retired: absent from this
documentation, and removed when the legacy backend shuts down. Don’t
build new code on them.

Installation changes too: one `PSReader.xcframework` plus the Apryse PDF
libraries, with ZIPFoundation no longer required. With CocoaPods, the
`PSReader` pod becomes `PSReaderUI2`, from the same specs repository.
See [Install the SDK](/documentation/PSReader/Getting-Started#Install-the-SDK).

Decide where you land first; [Choosing an Integration](/documentation/PSReader/Choosing-an-Integration) compares the
two sides. Whichever you choose, [Keeping Users’ Data](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#Keeping-Users-Data) covers the
downloads and saved pages your users already have.

## Moving to the Prebuilt UI

Replace your reader screen with the prebuilt one. Either replace your
archive and the screens around it too, with [`CarouselViewController`](/documentation/PSReader/CarouselViewController),
which loads your publications and opens editions, bookmarks, downloads
and search on its own:

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

Or keep your own archive, port its fetching as [Fetching the Catalog](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#Fetching-the-Catalog)
describes, and open the edition the user picks in the prebuilt reader
screen:

```swift
let reader = FeedReaderViewController(globalConfig: globalConfig, published: published)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

Either way, delete your `PSReaderViewController` screen with its delegates
and the article-fetching layer: the prebuilt reader brings its own
navigation bar, content browser, bookmarking, and settings. With the
carousel, `PSAPIController`, `PSBookMarkController`, and
`PSDownloadController` go as well, and so does your `setApiKey` call: the
carousel initializes the SDK with the key in your [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration).
With your own archive, keep an early `PSReader.initialize(apiKey:)` call
and await it before the archive’s first request, and consider [`BookmarksViewController`](/documentation/PSReader/BookmarksViewController) and
[`DownloadsViewController`](/documentation/PSReader/DownloadsViewController) for your bookmark and download lists.

The prebuilt screens don’t run the data migrations; see
[With the Prebuilt Screens](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#With-the-Prebuilt-Screens) for what they show of your users’
content. Continue with [Setting Up the Carousel](/documentation/PSReader/Setting-Up-the-Carousel) or
[Presenting the Prebuilt Reader](/documentation/PSReader/Presenting-the-Prebuilt-Reader). Apart from
[With the Prebuilt Screens](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#With-the-Prebuilt-Screens), the rest of this page is for a custom
UI.

## Moving to a Custom UI

Keep your own screens and port each legacy mechanism to the core SDK:
[`FeedEditionService`](/documentation/PSReader/FeedEditionService) for the catalog, a reader screen that hosts
[`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) and opens editions, and
[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager) and [`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager) for offline copies and
bookmarks. Start from the reader screen in [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader),
`ReaderScreenViewController`, and replace your `PSReaderViewController`
screen with it. Then work through the sections from
[The Shape of the Change](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#The-Shape-of-the-Change) on, each of which maps one mechanism, with
the old code beside the new, and migrate your users’ data as the next
section describes. [A Complete Migrated Integration](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#A-Complete-Migrated-Integration) puts it
together.

## Keeping Users’ Data

The legacy SDK kept three kinds of user content on the device, and each
carries over differently:

|Saved with the legacy SDK                 |In the current SDK                                                                                                                                                                                          |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Edition downloads (`PSDownloadController`)|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:)`` adds them to ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/downloads``.|
|Saved pages (`downloadPDFForPage`)        |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)`` turns them into page bookmarks.                                                               |
|Bookmarks (`PSBookMarkController`)        |No call migrates them.                                                                                                                                                                                      |

In a custom UI, call both migrations once at startup, on the main thread,
before you show downloads or bookmarks:

```swift
func application(_ application: UIApplication,
                 didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    PSEDownloadManager.shared.migrateLegacyDownloads()
    PSEBookmarkManager.shared.migrateLegacyPageBookmarks()
    return true
}
```

Each call reads the files the legacy SDK left on the device and uses no
network. It does its work once per install and returns immediately on
later calls, so it can stay in your launch code. If the legacy SDK’s list
exists but can’t be read yet, as before the device’s first unlock, the
next call tries again.

Migration leaves the legacy files where they are. Each migrated item gets
a *bridged* catalog entry ([`isBridged`](/documentation/PSReader/PSEPublished/isBridged)) built from what the
legacy SDK recorded: a migrated download reports
[`PSEDownloadManager.DownloadState.downloaded`](/documentation/PSReader/PSEDownloadManager/DownloadState/downloaded), and a migrated saved page
becomes a [`PSEBookmarkPage`](/documentation/PSReader/PSEBookmarkPage) whose [`isBridged`](/documentation/PSReader/PSEBookmarkPage/isBridged) is
`true`. The edition itself is built when it opens, from the files the
legacy SDK cached, falling back to the legacy backend for any it didn’t.

### Opening Migrated Editions

Open a bridged entry with [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition), and show it in
your reader screen with `ReaderScreenViewController(source:openingPage:)`.
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) can’t open a bridged entry,
and neither can `ReaderScreenViewController(published:openingPageGUID:)`,
which calls it. So wherever your app opens editions, such as your archive
screen, check [`isBridged`](/documentation/PSReader/PSEPublished/isBridged) first:

```swift
func readerScreen(for published: PSEPublished) async throws -> ReaderScreenViewController {
    if published.isBridged {
        // Migrated from the legacy SDK: open it through the bridge.
        let source = try await PSLegacyBridgedEdition.open(published: published)
        return ReaderScreenViewController(source: source)
    }

    // Anything else opens in the screen, with progress.
    return ReaderScreenViewController(published: published)
}
```

A migrated page bookmark opens the same way, at its page:

```swift
if let published = bookmark.published, published.isBridged {
    let source = try await PSLegacyBridgedEdition.open(published: published)
    let page = bookmark.pageGUID.flatMap { source.edition.page(forGUID: $0) }
    let screen = ReaderScreenViewController(source: source, openingPage: page)
}
```

The opened edition holds the legacy edition’s PDF pages in order,
followed by article pages that regions on the PDF pages open. The
migration hooks build those article pages.

### Customizing the Migration

Both migration calls take a [`PSLegacyMigrationHooks`](/documentation/PSReader/PSLegacyMigrationHooks) object, which
defaults to [`PSLegacyDefaultMigrationHooks`](/documentation/PSReader/PSLegacyDefaultMigrationHooks). Hooks don’t locate the
legacy files; the SDK reads those from where the legacy SDK always kept
them. Hooks run at two moments.

At migration, they choose what migrates and what each entry records:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/accountGUID`` and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/applicationGUID`` become each entry’s
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/accountGUID`` and ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/applicationGUID``, which
  holds the publication GUID. Both are empty by default.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/publicationGUID(forLegacyPublicationGUID:)``
  maps the legacy edition’s replica publication GUID to the entry’s
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/publicationGUID``. By default the entry keeps the replica
  publication GUID.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/shouldMigrate(edition:)`` can leave a download
  out; saved pages migrate without asking.
- For each download that migrates,
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/retainedLegacyCacheURLs(forEdition:)`` lists
  files your app cached through the legacy SDK for that edition, such as
  article feeds, so later cache refreshes don’t remove them.

When a migrated edition opens through [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition), they
build its article pages:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/migratedArticles(forEdition:legacyArticles:context:)``
  turns the legacy articles into ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigratedArticle`` values: the
  HTML of each article page and the regions on PDF pages that open it.
  By default, each article with a headline gets a plain page with its
  headline, byline, cached image, and body.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/additionalEditionResources(forEdition:)``
  supplies files that HTML references, such as stylesheets and fonts.

Write your own hooks for three reasons: to record your publication’s
identity, so code that filters or reports editions by publication treats
migrated entries like the rest; to leave editions out; or to present
migrated articles your way. Implement only what you change:

```swift
final class MigrationHooks: PSLegacyMigrationHooks {
    let accountGUID = "ACCOUNT_GUID"
    let applicationGUID = "PUBLICATION_GUID"

    // Leave out editions the legacy system flagged as encrypted.
    func shouldMigrate(edition: PSLegacyEditionSummary) -> Bool {
        !edition.isEncrypted
    }
}

let hooks = MigrationHooks()
PSEDownloadManager.shared.migrateLegacyDownloads(hooks: hooks)
PSEBookmarkManager.shared.migrateLegacyPageBookmarks(hooks: hooks)
```

Migration runs once, so settle the hooks before you ship: entries keep the
identity they were given, and an edition left out isn’t offered again.
Article hooks take effect only in editions you open with
[`open(published:hooks:onProgress:)`](/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:)) and your
hooks, so pass them in `readerScreen(for:)` above:
`PSLegacyBridgedEdition.open(published: published, hooks: hooks)`.
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) never uses your hooks.

### With the Prebuilt Screens

The prebuilt screens, in the carousel or on their own, don’t run these
migrations and don’t open editions through [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition), so
leave the calls out when users reach their content through those screens.
The screens read the legacy SDK’s records directly instead: when their
content types include legacy replica content, as `.all` does,
[`DownloadsViewController`](/documentation/PSReader/DownloadsViewController) lists the legacy SDK’s downloads and
[`BookmarksViewController`](/documentation/PSReader/BookmarksViewController) its bookmarks, and both open them in the
replica reader. Calling [`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:))
as well would list each download twice. Pages saved with
`downloadPDFForPage` have no prebuilt screen.

## The Shape of the Change

From here on, each section ports one legacy mechanism to a custom UI.

The legacy SDK was one object: `PSReaderViewController` fetched,
downloaded, rendered, and navigated, with `PSAPIController`,
`PSBookMarkController`, and `PSDownloadController` singletons around it.
The core SDK splits those roles:

|Role                    |Legacy SDK                                |Current SDK                                                                                                                                      |
|------------------------|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
|Catalog requests        |`PSAPIController.requestPublication`      |``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService``                                                                       |
|Catalog entry           |`PSEdition` (stub, inside `PSPublication`)|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished``                                                                             |
|Loaded content          |`PSEdition` (populated by `load`)         |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEdition`` via a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEditionSource``|
|Rendering and navigation|`PSReaderViewController`                  |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController``                                                            |
|Offline copies          |`PSDownloadController`                    |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager``                                                                       |
|Bookmarks               |`PSBookMarkController`                    |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager``                                                                       |

One published edition is identified by [`publishedGUID`](/documentation/PSReader/PSEPublished/publishedGUID).

### Migration Checklist

1. Swap the frameworks and imports (`import PSReader`).
1. Replace `setApiKey` with `initialize` (below).
1. Replace catalog fetching with ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService``.
1. Replace your reader screen with `ReaderScreenViewController`:
   creation, loading, delegates, navigation.
1. Delete the article-fetching layer; articles are now in the page flow.
1. Port bookmarks and downloads to the managers.
1. Migrate your users’ downloads and saved pages, and open bridged
   entries (see <doc://com.pagesuite.PSReader/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#Keeping-Users-Data>).
1. Delete the old NotificationCenter observers and thumbnail requests.

## Initialization

```swift
// Legacy SDK
PSAPIController.sharedController.setApiKey(apiKey) { success in ... }

// Current SDK: call it once at launch; there's no need to wait for it
PSReader.initialize(apiKey: apiKey)
```

Call it once at launch and carry on; the SDK waits for it where it needs
to. See [Initialize the SDK](/documentation/PSReader/Getting-Started#Initialize-the-SDK).

## Fetching the Catalog

```swift
// Legacy SDK: a publication with stub editions, newest first, capped by archiveLimit
PSAPIController.sharedController.requestPublication("REPLICA_PUBLICATION_GUID", archiveLimit: 30) { publication, error in
    let editions = publication?.editions
}

// Current SDK: published editions grouped by date, newest first
let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
let archive = try await service.publishedEditions(
    publicationGUID: "PUBLICATION_GUID",
    publicationName: "The Daily"   // copied onto each edition, for your titles
)
let editions = archive.flatMap { $0.editions ?? [] }   // flat, newest first
let latest = archive.latestEdition
```

Differences:

- `publicationGUID:` takes the publication GUID on the current system, a
  new value, not the replica publication GUID.
- There is no `archiveLimit`: the service returns the publication’s
  archive window; truncate locally if you showed fewer.
- The month-filtered variant (`requestPublicationForMonth`) is gone. The
  results arrive grouped into ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublishedDate`` buckets, so month
  filtering is a local `filter` over `date`, and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService/publishedEditions(publicationGUID:publicationName:startDate:endDate:pageNumber:pageSize:)``
  fetches a date range.
- Deep links and search results that carry only an edition GUID resolve
  through ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionService/published(forEditionGUID:)``.

## Creating the Reader and Loading an Edition

```swift
// Legacy SDK
let psReader = PSReaderViewController()
psReader.delegate = self
psReader.spineLocation = .mid            // double-page mode
addChild(psReader); view.addSubview(psReader.view)
psReader.loadEdition(edition)            // stub PSEdition from the publication

// Current SDK: your reader screen hosts the reader and opens the edition
let screen = ReaderScreenViewController(published: published)
present(UINavigationController(rootViewController: screen), animated: true)
```

`ReaderScreenViewController` is the reader screen from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader). The code in the sections below runs inside it,
where `reader` is the hosted [`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) and
`source` is the open edition. Its `hostReader()` adds the reader as a
child, as before, and sets the delegates that replace
`PSReaderViewControllerDelegate` and `spineLocation`.

Loading is now explicit and two-step, and the screen does both steps:
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) resolves the content (a
downloaded copy when present, otherwise a stream from the network,
throwing when neither is possible), and
[`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:))
shows it. An opening page replaces post-load `scrollToPage` calls when you
enter at a known page: `ReaderScreenViewController(published:openingPageGUID:)`
takes its GUID.

**Spine location → layout delegate.** `spineLocation = .none/.mid` (and the
per-orientation `spineLocationPortrait`/`spineLocationLandscape`) become a
single callback the reader consults on every layout change. The reader
screen’s version shows facing pages on a wide screen in landscape; for the
old landscape `.mid` behavior on every device, return:

```swift
func pagingMode(forTraits traits: UITraitCollection, size: CGSize) -> PSEditionPagingMode {
    size.width > size.height ? .double : .single
}
```

Without a layout delegate the reader stays single-page.

## Page-Change Events

```swift
// Legacy SDK: two callbacks with different numbering
func didChangeToPage(_ page: Int) { }   // page index, 0-based
func pageScrollTo(_ page: Int) { }      // page number, 1-based

// Current SDK: one delegate, spread-based
func willScrollTo(pageIndex: Int, pagingMode: PSEditionPagingMode, source: Any?) { }
func didSettleOn(pageIndex: Int, pagingMode: PSEditionPagingMode) { }
```

The indices are **spread** indices: in double-page mode one index covers
two facing pages (`pageIndex` counts screens, not sheets). The reader
screen’s `didSettleOn` calls `updateChrome()`, which reads the settled page
and shows its label:

```swift
pageLabel.text = "Page \(page.pageLabel)"
```

[`pageLabel`](/documentation/PSReader/PSEPage/pageLabel) is the label the publisher printed, such as “A3”,
and the page number when the edition has none. Use it rather than
[`pageNumber`](/documentation/PSReader/PSEPage/pageNumber), which ignores the publisher’s labels and reports
`0` for advert pages; see [The Edition Model](/documentation/PSReader/The-Edition-Model).

Programmatic navigation maps directly: `scrollToPage(index)` →
[`scrollTo(index:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(index:source:)) (spread index),
plus richer overloads by page, GUID, article, and section.
`scrollToNextPage`/`scrollToPrevPage` become `scrollTo(index:)` arithmetic
on the current spread index.

Zoom reporting moved onto the same delegate:
`PSReaderZoomDelegate.readerDidZoom(zoomLevel:)` becomes the optional
`didZoom(toScale:pageIndex:pagingMode:)`, which fires when a zoom gesture
**ends** rather than continuously, so expect fewer events.

## Articles

The legacy SDK’s article machinery is gone because articles no longer live
outside the page flow. In the legacy SDK you fetched them, listened for
taps, fetched content, and presented your own view:

```swift
// Legacy SDK: DELETE ALL OF THIS
PSAPIController.sharedController.requestArticlesForEdition(edition) { ... }
psReader.articleDelegate = self
func loadArticle(_ articleID: String?) {
    // find PSArticle, requestArticleDetails, present article.body yourself
}
```

On the current system, articles are **pages**: templated HTML pages
([`type`](/documentation/PSReader/PSEPage/type) `templateArticle`) that the reader renders in-flow, with
hotspot links on PDF pages jumping straight to them. There is nothing to
fetch and nothing to present.

What remains for you:

- **Reading article data** (analytics, sharing, TTS): the model is on the
  page, in ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/articles``, and the body HTML is ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEArticle/story``
  (the legacy SDK called it `body`). `headline`, `author`, and `sharelink`
  keep their roles; the casing of `articleguid` and `sharelink` is
  contract.
- **Reacting to article taps** on PDF pages: the default hotspot overlay
  jumps the reader itself; observe
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/willScrollTo(pageIndex:pagingMode:source:)``,
  where the jump arrives tagged with an ``doc://com.pagesuite.PSReader/documentation/PSReader/ArticleJumpNavigationSource``.

## Sections

```swift
// Legacy SDK
let sections = psReader.currentEdition.sections

// Current SDK, in your reader screen
guard let source else { return }
let sections = source.edition.sections ?? []      // [PSESection]
if let section = sections.first {
    reader.scrollTo(section: section)             // jump to a section
}
```

[`PSESection`](/documentation/PSReader/PSESection) keeps `name` and adds `color`, `logourl`, and its
[`articles`](/documentation/PSReader/PSESection/articles).

## Bookmarks

`PSBookMarkController`’s page-index-based API becomes
[`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager), keyed on model objects, with articles and pages
unified behind one context type:

|Legacy SDK                                   |Current SDK                                                                                                                      |
|---------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
|`toggleBookmark(index, edition:)`            |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/toggleBookmark(context:edition:published:application:)``|
|`hasBookmark(edition, index:)`               |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/isBookmarked(context:)``                                |
|`createBookmarkForPageIndexInEdition`        |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/addBookmark(forPage:edition:published:application:)``   |
|`getBookmarks()` (dictionary)                |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/bookmarks`` (flat, typed)                               |
|`getBookmarksForEdition(_:)`                 |`bookmarks.filter { $0.published?.editionGUID == … }`                                                                            |
|`deleteBookMark(bookmark:)`                  |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeBookmark(_:)-5vc38``                              |
|`clearBookmarks()`                           |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeAllBookmarks()``                                  |
|article variants (`toggleArticleBookmark`, …)|the same context API; a context wraps either kind                                                                                |

Bookmarks saved with `PSBookMarkController` don’t carry over; see
[Keeping Users’ Data](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#Keeping-Users-Data).

A bookmark button follows the page on screen from the reader screen’s
`updateChrome()`, and toggles the bookmark through
[`toggleBookmark(context:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(context:edition:published:application:)).
[Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button) builds it.

Change observation replaces polling: conform to [`PSEBookmarkObserver`](/documentation/PSReader/PSEBookmarkObserver)
(all methods optional) or observe
[`bookmarksDidChange`](/documentation/PSReader/PSEBookmarkManager/bookmarksDidChange).

Opening a saved bookmark, including the offline case the legacy SDK had
no answer for, is one call:

```swift
let (source, openingPage) = try await bookmark.editionSource()
let screen = ReaderScreenViewController(source: source, openingPage: openingPage)
```

It opens the bookmark’s own edition at the saved page when that edition is
available (downloaded or online), else falls back to a
[`PSEBookmarksEdition`](/documentation/PSReader/PSEBookmarksEdition) synthesized from the saved content. Open migrated
page bookmarks as [Opening Migrated Editions](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#Opening-Migrated-Editions) shows.

## Downloads

`PSDownloadController`’s queue and NotificationCenter contract becomes
[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager) with a typed observer:

|Legacy SDK                                                                    |Current SDK                                                                                                                                                                                                                       |
|------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`queueEditionForDownload(edition)`                                            |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/queueDownload(published:)``                                                                                                                              |
|`getDownloadList()` / `retrieveDownloads()`                                   |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/downloads``                                                                                                                                              |
|`cancelCurrentDownload(editionGUID:)`                                         |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/cancelDownload(for:)``                                                                                                                                   |
|`cancelAllDownloads()`                                                        |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/cancelAllDownloads()``                                                                                                                                   |
|`deleteDownload(_:completion:)`                                               |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/removeDownload(for:)``                                                                                                                                   |
|`"PSDownloadStarted"` and `"PSDownloadProgressed-<id>"` notifications         |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/downloading(phase:phaseProgress:globalProgress:)``                                                                                         |
|`"PSDownloadFinished"` notification                                           |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/downloaded``                                                                                                                               |
|`"PSDownloadErrored"` notification                                            |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/errored``                                                                                                                                  |
|`"PSDownloadDeleted"` notification                                            |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/notDownloaded``; the manager never reports ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEDownloadManager/DownloadState/deleted``|
|`downloadPDFForPage(_:useOriginalPDFs:completion:)`, `retrievePageDownloads()`|a page bookmark: ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/addBookmark(forPage:edition:published:application:)`` stores the page’s files with the bookmark                                         |

Every state arrives through one [`PSEDownloadObserver`](/documentation/PSReader/PSEDownloadObserver) callback:

```swift
// Legacy SDK: five stringly named notifications, some suffixed per edition
NotificationCenter.default.addObserver(forName:
    NSNotification.Name("\(PSReaderConfig.kPSDownloadNotificationProgressedKey)-\(edition.id)"),
    object: nil, queue: .main) { note in ... }

// Current SDK: register per edition (returns the current state) or globally
let state = PSEDownloadManager.shared.addObserver(self, published: published)

func downloadManager(_ manager: PSEDownloadManager,
                     downloadFor published: PSEPublished,
                     didChangeState state: PSEDownloadManager.DownloadState) {
    switch state {
    case .downloading(_, _, let globalProgress): progressBar.progress = globalProgress
    case .downloaded: showDone()
    case .errored: offerRetry()   // queue again to retry; no error payload
    default: break
    }
}
```

Behind a download button, [`toggleDownloadState(for:)`](/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:))
performs the queue, cancel, or delete transition in one call and throws
[`PSDownloadError`](/documentation/PSReader/PSDownloadError) when connectivity policy forbids starting. Once a
download completes, `openEditionSource()` prefers it automatically;
nothing else in the opening flow changes.

## Thumbnails and Page Images

The image request layer is gone; the URLs are on the models:

```swift
// Legacy SDK
PSAPIController.sharedController.requestThumbnailImage(edition: id, size: size) { image in ... }

// Current SDK: the cover URL is on the catalog entry
cell.load(url: URL(string: published.image))
```

Per-page images (`requestPageImage`) become [`effectiveScreenshotURL`](/documentation/PSReader/PSEPage/effectiveScreenshotURL),
resolved through the edition source’s [`resourceManager`](/documentation/PSReader/PSEEditionSource/resourceManager)
so downloaded editions read from disk and streamed ones fetch on demand.
See [Building a Page Browser](/documentation/PSReader/Building-a-Page-Browser) for the full browser.

## Adverts

Legacy banner adverts under the reader
(`PSReaderAdvertDelegate.bannerAd(forPageNumber:) -> UIView?`) have no
successor inside the reader: a persistent banner is host chrome now, so
place your banner view in your own hierarchy around the reader.

What the reader supports instead is **in-flow advert pages**: dedicated
pages in the edition ([`isAdvertPage`](/documentation/PSReader/PSEPage/isAdvertPage)). HTML and image creatives
render out of the box; supply
[`PSEditionReaderViewController.AdvertDelegate`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol) to serve them from your
own ad stack, such as Google Ad Manager. See [Handling Advert Pages](/documentation/PSReader/Handling-Advert-Pages).

## Links

The legacy SDK opened tapped hyperlinks itself. The current reader opens
`mailto:` links and posts most others in
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification), for your app to
open however it prefers. Without an observer, those links do nothing. See
[Opening Links](/documentation/PSReader/Hosting-the-Reader#Opening-Links).

## Not Carried Over

- **Right-to-left reading** (`rightToLeft`) has no equivalent in the
  current reader today. If you publish right-to-left titles, talk to your
  account manager before scheduling a migration.
- **The download notification keys** don’t fire for downloads made with
  the current SDK; the typed observer above replaces them.
- **Reader appearance tweaks** (`useOriginalPages`, `stayZoomedIn`,
  `loadingInfoViewText`, edge-fill flags) have no direct equivalents; the
  loading UI is entirely yours now, and PDF fitting is
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/pdfLayoutMode``.

## A Complete Migrated Integration

A minimal custom UI, assembled from the sections above: an edition list
that migrates your users’ data once, then opens any entry, migrated ones
included, in the reader screen from [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader).

```swift
import PSReader
import UIKit

/// Your archive screen: one row per edition.
final class EditionListViewController: UITableViewController {

    private let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
    private var editions: [PSEPublished] = []

    override func viewDidLoad() {
        super.viewDidLoad()
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "Edition")

        Task {
            // The app delegate initialized the SDK at launch.
            PSEDownloadManager.shared.migrateLegacyDownloads()
            PSEBookmarkManager.shared.migrateLegacyPageBookmarks()

            do {
                let archive = try await service.publishedEditions(
                    publicationGUID: "PUBLICATION_GUID",
                    publicationName: "The Daily"
                )
                editions = archive.flatMap { $0.editions ?? [] }
                tableView.reloadData()
            } catch {
                showAlert(title: "Couldn't Load Editions", error: error)
            }
        }
    }

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        editions.count
    }

    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "Edition", for: indexPath)
        cell.textLabel?.text = editions[indexPath.row].name
        return cell
    }

    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        tableView.deselectRow(at: indexPath, animated: true)
        open(editions[indexPath.row])
    }

    /// Opens any catalog entry, including one migrated from the legacy SDK.
    func open(_ published: PSEPublished) {
        Task {
            do {
                let screen = try await readerScreen(for: published)
                let navigationController = UINavigationController(rootViewController: screen)
                navigationController.modalPresentationStyle = .fullScreen
                present(navigationController, animated: true)
            } catch {
                showAlert(title: "Couldn't Open Edition", error: error)
            }
        }
    }

    private func readerScreen(for published: PSEPublished) async throws -> ReaderScreenViewController {
        if published.isBridged {
            // Migrated from the legacy SDK: open it through the bridge.
            let source = try await PSLegacyBridgedEdition.open(published: published)
            return ReaderScreenViewController(source: source)
        }

        // Anything else opens in the screen, with progress.
        return ReaderScreenViewController(published: published)
    }
}
```

The reader screen shows the page label and chooses single or double
pages. Add a download button and a bookmark button to it
([Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button), [Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button)), a
downloads list over [`downloads`](/documentation/PSReader/PSEDownloadManager/downloads) that opens each entry
with the same `open(_:)`, and link handling
([Opening Links](/documentation/PSReader/Hosting-the-Reader#Opening-Links)), and the legacy feature set is
covered.

## Going Deeper

Each mechanism has a full guide in [Custom UI](/documentation/PSReader/Custom-UI):
[Fetching the Archive](/documentation/PSReader/Fetching-the-Archive), [Opening an Edition](/documentation/PSReader/Opening-an-Edition),
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader), [Building a Page Browser](/documentation/PSReader/Building-a-Page-Browser),
[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps), [Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button), and
[Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button).

## Topics

### Migration Hooks

[`PSLegacyMigrationHooks`](/documentation/PSReader/PSLegacyMigrationHooks)

Customizes how content saved with the legacy SDK migrates to the current
SDK.

