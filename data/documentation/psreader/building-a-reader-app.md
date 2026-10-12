<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Building-a-Reader-App",
  "metadataVersion" : "0.1.0",
  "role" : "sampleCode",
  "title" : "Building a Reader App"
}
-->

# Building a Reader App

Build a reader app both ways in a sample project: with the prebuilt UI,
then with your own reader screen on the core SDK.

## Overview

The sample is one Xcode project with two small apps, one for each side of
the SDK. Both read PAG802, PageSuite’s demo publication:

|App     |Side       |What it shows                                                        |Code                                                                    |
|--------|-----------|---------------------------------------------------------------------|------------------------------------------------------------------------|
|Prebuilt|Prebuilt UI|The carousel, and your own archive screen opening the prebuilt reader|`Prebuilt/SceneDelegate.swift`, `Shared/EditionListViewController.swift`|
|Custom  |Custom UI  |The same archive screen, opening your own reader screen              |`Custom/`, `Shared/EditionListViewController.swift`                     |

Both apps share the app delegate and the archive screen in `Shared/`.
The Prebuilt app adds only its scene delegate, and the Custom app adds
its reader screen, so moving from one side to the other changes one
closure and the reader screen behind it. [Choosing an Integration](/documentation/PSReader/Choosing-an-Integration) compares the two
sides.

## Configure the Sample Code Project

1. In the `Config` folder, copy `Secrets.xcconfig.example` to
   `Secrets.xcconfig` and replace `API_KEY` with your API key. Git ignores
   `Secrets.xcconfig`, so your key stays out of source control.
1. Open `PSReaderSample.xcodeproj`.
1. Choose the **Prebuilt** or **Custom** scheme, and run it on a simulator
   or a device running iOS 15 or later.

The apps link the SDK the way your app will, as a binary through Swift
Package Manager, and import one module, `PSReader`. Both initialize it at
launch, in `Shared/AppDelegate.swift`, without waiting for it:

```swift
// Initialize the SDK once, at launch. There's no need to wait for it.
PSReader.initialize(apiKey: Sample.apiKey)
```

[Getting Started](/documentation/PSReader/Getting-Started) explains initialization.

Every identifier the apps use, from the shortcode to the publication GUIDs,
is in `Shared/Sample.swift`.

## Show the Carousel

The Prebuilt app’s first tab is the carousel: the SDK’s complete reader
experience in one view controller, with the archive, the reader,
bookmarks and downloads. It needs your credentials in a
[`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration), which the scene delegate keeps as a property:

```swift
// Your credentials, plus your fonts, colors and delegates when you
// need them. Every prebuilt screen takes this configuration.
private var globalConfig = GlobalConfiguration(
    apiKey: Sample.apiKey,
    accountGUID: Sample.accountGUID
)
```

And the sections to show:

```swift
// The carousel builds the archive from your shortcode, and opens the
// reader, bookmarks and downloads on its own.
let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: Sample.shortcode),
        .subsections("My Content", [
            .init(name: "Bookmarks", type: .bookmarks(type: .all)),
            .init(name: "Downloads", type: .downloads(type: .all))
        ])
    ]
)
```

![The sample's Prebuilt app showing the carousel with the demo publication's editions.](images/com.pagesuite.PSReader/sample-prebuilt-carousel~dark@2x.png)

`.dynamicArchive` reads the archive’s layout from your app’s configuration
at PageSuite, so PAG802’s three publications appear as three subsections
without any GUIDs in your code. In an app that only needs the carousel,
make it the window’s root view controller instead of a tab:

```swift
window?.rootViewController = carousel
```

To choose sections and content types yourself, see
[Setting Up the Carousel](/documentation/PSReader/Setting-Up-the-Carousel). To match your brand, see [Theming](/documentation/PSReader/Theming).

## Open the Prebuilt Reader From Your Own Screen

Your app may have screens of its own, such as a home page or a list of
titles, and want only the reader from the SDK. The Prebuilt app’s second
tab is an archive screen the app draws itself, `EditionListViewController`,
which opens the prebuilt reader.

The list gets its editions from [`FeedEditionService`](/documentation/PSReader/FeedEditionService), one request for
each publication:

```swift
// This list loads the moment the app starts. Until the SDK
// waits for its own initialization before a catalog request,
// make sure it has finished; it returns at once afterwards.
await PSReader.initialize(apiKey: Sample.apiKey)

var archive: [(publication: Sample.Publication, editions: [PSEPublished])] = []

// The service returns editions grouped by publishing date,
// newest first, and editions published on the same day in
// the backend's order. This list only needs them in order.
// Passing the publication's name puts it on each edition,
// for the reader screen's title.
for publication in Sample.publications {
    let dates = try await service.publishedEditions(
        publicationGUID: publication.guid,
        publicationName: publication.name
    )
    archive.append((publication, dates.flatMap { $0.editions ?? [] }))
}
```

![The sample's own edition list, grouped by look, which opens the prebuilt reader.](images/com.pagesuite.PSReader/sample-prebuilt-edition-list@2x.png)

Each [`PSEPublished`](/documentation/PSReader/PSEPublished) carries what a row shows: its `name`, its
`datePublished`, and [`image`](/documentation/PSReader/PSEPublished/image), the URL of its cover. The
sample formats the date itself; to match the prebuilt archive’s dates,
use the formatter [Date Formatting](/documentation/PSReader/Theming#Date-Formatting) describes. The
carousel found the publications through the shortcode; your own screens
name them by account GUID and publication GUID. [Identifiers](/documentation/PSReader/Identifiers) explains
where each identifier comes from.

A tap presents [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController), the reader screen the carousel
uses, on the tapped edition:

```swift
let editions = EditionListViewController { [unowned self] published, list in
    let reader = FeedReaderViewController(globalConfig: self.globalConfig, published: published)
    reader.modalPresentationStyle = .fullScreen
    list.present(reader, animated: true)
}
```

The carousel’s dynamic archive loads your app configuration, but only for
the carousel’s own readers. A reader you open yourself takes it from
[`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig), so the app loads it with
[`AppConfigService`](/documentation/PSReader/AppConfigService) once its window is up:

```swift
// The carousel's dynamic archive loads your app configuration for
// the carousel's own readers. Readers you open yourself read it
// from the global configuration, so load it for them too: some of
// the demo's pages show the masthead logo it names.
Task {
    globalConfig.remoteConfig = try? await AppConfigService().configuration(forShortcode: Sample.shortcode)
}
```

`globalConfig` is a property of the scene delegate, which the tap reads
when it creates a reader, so every reader created after the configuration
loads gets it. [Presenting the Prebuilt Reader](/documentation/PSReader/Presenting-the-Prebuilt-Reader) says which features
read it. The Custom app loads none: its reader screen would take the logo
from a media delegate rather than the configuration, and the demo uses
none of the features that read the configuration there; see
[Passing the App Configuration](/documentation/PSReader/Hosting-the-Reader#Passing-the-App-Configuration).

The reader brings its own navigation bar, content browser, bookmarks and
settings, and it takes the same `globalConfig` as the carousel, so both
tabs look and behave alike. To open the latest edition, or an edition from
a link, see [Presenting the Prebuilt Reader](/documentation/PSReader/Presenting-the-Prebuilt-Reader). For more on the catalog,
see [Fetching the Archive](/documentation/PSReader/Fetching-the-Archive).

## Build Your Own Reader Screen

The Custom app keeps the archive screen and changes what a tap does. It
presents `ReaderScreenViewController`, a reader screen of the app’s own,
inside a navigation controller for its bars:

```swift
let editions = EditionListViewController { published, list in
    let reader = UINavigationController(rootViewController: ReaderScreenViewController(published: published))
    reader.modalPresentationStyle = .fullScreen
    list.present(reader, animated: true)
}
```

![The sample's custom reader showing a classic PDF page with the app's own title, page label, and bookmark and download buttons.](images/com.pagesuite.PSReader/sample-custom-reader~dark@2x.png)

`ReaderScreenViewController` uses only the core SDK. A
[`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) draws the edition’s pages, and the app
draws everything else: a navigation bar with a close button, the
publication’s name, and download and bookmark buttons, plus a toolbar with
the page label. [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader) presents the same class, and the guides in
[Custom UI](/documentation/PSReader/Custom-UI) add to it. The sections below follow it in the order the
Custom UI hub builds a reader.

### Host the Reader

The edition reader is a child of your reader screen, never shown on its
own. Add it like any child view controller, then set its delegates before
opening anything:

```swift
private func hostReader() {
    // The reader is a child of this screen, never shown on its own.
    addChild(reader)
    view.addSubview(reader.view)
    reader.view.translatesAutoresizingMaskIntoConstraints = false

    NSLayoutConstraint.activate([
        reader.view.leadingAnchor.constraint(equalTo: view.leadingAnchor),
        reader.view.trailingAnchor.constraint(equalTo: view.trailingAnchor),
        reader.view.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor),
        reader.view.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor)
    ])

    reader.didMove(toParent: self)

    // Set the delegates before opening an edition, so the reader uses
    // them from the first page. The scroll delegate reports the page on
    // screen; the layout delegate chooses single or double pages.
    reader.scrollDelegate = self
    reader.layoutDelegate = self
}
```

The sample keeps the pages between its bars. [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader)
shows how to float chrome over the pages instead, and hide it as the user
scrolls.

### Open the Edition

[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) turns the tapped edition
into a source the reader can show. It opens the downloaded copy when there
is one and streams the edition otherwise, so the screen needs no offline
logic of its own. The screen shows a spinner until a streamed edition
reports progress, then a progress bar:

```swift
private func openEdition() {
    // A spinner until the edition reports progress. A downloaded
    // edition opens without reporting any.
    activityIndicator.startAnimating()
    progressView.progress = 0
    progressView.isHidden = true

    Task {
        do {
            // Opens the downloaded copy if there is one, and otherwise
            // streams the edition, reporting progress as its opening
            // pages download.
            let source = try await published.openEditionSource { progress in
                self.activityIndicator.stopAnimating()
                self.progressView.isHidden = false
                self.progressView.setProgress(progress, animated: true)
            }

            let page = openingPageGUID.flatMap { source.edition.page(forGUID: $0) }
            show(source, at: page)
        } catch {
            stopLoading()
            showAlert(title: "Couldn't Open Edition", error: error, retry: openEdition)
        }
    }
}

private func show(_ source: PSEEditionSource, at page: PSEPage?) {
    self.source = source
    reader.open(edition: source, openingPage: page)
    stopLoading()
    updateChrome()
}
```

Opening has no side effects to undo, so retrying is calling it again.
[Opening an Edition](/documentation/PSReader/Opening-an-Edition) covers the other ways to open an edition.

The screen’s title is the publication’s name, which the archive screen
put on each edition by passing `publicationName:`. An edition resolved
from its GUID alone has none, so the screen falls back to the edition’s
name:

```swift
// The publication's name, which the catalog fills in when you pass
// `publicationName:`. An edition resolved from its GUID alone
// doesn't have one, so fall back to the edition's name.
title = published.publicationName.isEmpty ? published.name : published.publicationName
```

### Follow the Reader

The reader’s [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) reports when
the reader settles on a page, and the sample’s `didSettleOn` calls
`updateChrome()`:

```swift
func didSettleOn(pageIndex: Int, pagingMode: PSEditionPagingMode) {
    updateChrome()
}
```

`updateChrome()` reads the current page and updates the page label and
the bookmark button:

```swift
/// Shows the current page's label and bookmark state.
private func updateChrome() {
    guard let page = reader.currentPage() else {
        return
    }

    // A friendly label, such as "A3", when the edition has one, and
    // otherwise the page number.
    pageLabel.text = "Page \(page.pageLabel)"
    pageLabel.sizeToFit()

    // Some pages, such as section fronts and adverts, have nothing
    // to bookmark.
    let context = page.bookmarkContext()
    let isBookmarked = PSEBookmarkManager.shared.isBookmarked(context: context)
    bookmarkButton.isEnabled = context.isBookmarkable
    bookmarkButton.image = UIImage(systemName: isBookmarked ? "bookmark.fill" : "bookmark")
}
```

### Show Facing Pages

On a wide screen in landscape, such as an iPad, the sample shows a
classic PDF edition’s facing pages side by side, the way they were
printed. The reader asks its [`PSEditionReaderViewController.LayoutDelegate`](/documentation/PSReader/PSEditionReaderViewController/LayoutDelegate-swift.protocol)
on every layout change:

```swift
/// Facing pages side by side on a wide screen, the way classic PDF
/// editions were printed; one page at a time otherwise.
func pagingMode(forTraits traits: UITraitCollection, size: CGSize) -> PSEditionPagingMode {
    traits.horizontalSizeClass == .regular && size.width > size.height ? .double : .single
}
```

Responsive editions show one page at a time whatever the delegate returns.
In double-page mode, `reader.currentPage()` is the page that best
represents the spread, so the page label and the bookmark button follow
the editorial page rather than an advert beside it.

### Open Links

The reader opens `mailto:` links itself and posts most other links for
the app to open. The sample follows them while its reader screen is on
screen:

```swift
override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(animated)

    // The reader leaves most links for the app to open, and posts them
    // app-wide. Follow them only while this screen is on screen.
    NotificationCenter.default.addObserver(
        self,
        selector: #selector(linkTapped),
        name: PSEditionReaderViewController.linkTappedNotification,
        object: nil
    )
}

override func viewDidDisappear(_ animated: Bool) {
    super.viewDidDisappear(animated)

    NotificationCenter.default.removeObserver(
        self,
        name: PSEditionReaderViewController.linkTappedNotification,
        object: nil
    )
}
```

It opens web links in an in-app Safari view, and anything else, such as a
`tel:` link, through the system, since a Safari view controller takes
only web URLs:

```swift
/// Opens a link the user tapped in the edition: web links in Safari
/// inside the app, and anything else, such as `tel:`, through the
/// system.
@objc private func linkTapped(_ notification: Notification) {
    guard let url = notification.userInfo?[PSEditionReaderViewController.linkTappedURLKey] as? URL else {
        return
    }

    switch url.scheme?.lowercased() {
    case "http", "https":
        present(SFSafariViewController(url: url), animated: true)
    default:
        // Safari view controllers take only web URLs.
        UIApplication.shared.open(url)
    }
}
```

[Opening Links](/documentation/PSReader/Handling-Media-and-Link-Taps#Opening-Links) lists which links the
reader opens itself and which it posts.

### Add a Download Button

`DownloadButton` is a bar button item that follows one edition through
[`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager). Observing an edition returns its current state, so
the button draws itself straight away, and the manager reports every
change after that to the button’s [`PSEDownloadObserver`](/documentation/PSReader/PSEDownloadObserver) method:

```swift
// Observing one edition returns its current state, so the button
// can draw itself before the first update arrives.
render(PSEDownloadManager.shared.addObserver(self, published: published))
```

A tap calls [`toggleDownloadState(for:)`](/documentation/PSReader/PSEDownloadManager/toggleDownloadState(for:)), which does
what a download button should for the current state:

```swift
@objc private func toggleDownload() {
    do {
        // Queues, cancels or deletes, depending on the current state.
        try PSEDownloadManager.shared.toggleDownloadState(for: published)
    } catch {
        onError?(error)
    }
}
```

Once an edition is downloaded, `openEditionSource` opens the stored copy,
so the edition opens offline with no change to the opening code. See
[Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button).

### Add a Bookmark Button

This is the sample’s whole bookmark button. If you’re building on the
host from [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader), follow [Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button)
instead of copying both.

[`bookmarkContext()`](/documentation/PSReader/PSEPage/bookmarkContext()) says what a page offers to bookmark: a page
showing one article bookmarks that article, and a PDF page bookmarks the
whole page. [`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager) adds or removes the bookmark:

```swift
@objc private func toggleBookmark() {
    guard let source, let page = reader.currentPage() else {
        return
    }

    do {
        // A page showing one article bookmarks the article; any other
        // page bookmarks the whole page.
        try PSEBookmarkManager.shared.toggleBookmark(
            context: page.bookmarkContext(),
            edition: source.edition,
            published: source.published
        )
    } catch {
        showAlert(title: "Couldn't Bookmark Page", error: error)
    }

    updateChrome()
}
```

Bookmarks keep enough of their content to reopen without a network
connection. To list them and open them again, see
[Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button).

## Read Every Kind of Edition

The archive screen has a section for each look PAG802’s editions have:
classic PDF, classic PDF with article pages, and responsive. All three
publications are on PageSuite’s current edition system, and both apps
open all three, the custom reader screen included.
[Edition Platforms](/documentation/PSReader/Edition-Platforms) explains how looks and systems relate.

## Use Your Own Publication

To see your own editions, change the identifiers in `Shared/Sample.swift`:

- `shortcode`, for the carousel’s dynamic archive;
- `accountGUID`, for every screen;
- `publications`, the publication GUIDs your own screens list, each with a
  section title.