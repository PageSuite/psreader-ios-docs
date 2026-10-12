<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Hosting-the-Reader",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Hosting the Reader"
}
-->

# Hosting the Reader

Build your own reader screen around the SDK’s edition reader: the screen
every custom-UI guide adds to.

## Overview

[`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) renders an edition’s pages and nothing
else: no navigation bar, page browser, or settings. Your reader screen
hosts it as a child view controller and draws the chrome around it. Using
the prebuilt reader? See [Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen).

`ReaderScreenViewController` below is that screen, as the sample app
builds it (see [Building a Reader App](/documentation/PSReader/Building-a-Reader-App)). It opens an edition with a
loading indicator, hosts the reader, and shows the publication’s name, a
close button, and the page label. It works the same for classic PDF and
responsive editions. Start from this class: every guide in [Custom UI](/documentation/PSReader/Custom-UI)
adds to it.

```swift
import PSReader
import UIKit

/// Your reader screen: the SDK's edition reader, hosted with your own
/// chrome around it.
final class ReaderScreenViewController: UIViewController {

    let reader = PSEditionReaderViewController()

    /// The open edition, once it has opened.
    private(set) var source: PSEEditionSource?

    private let published: PSEPublished
    private let openingPageGUID: String?
    private var openingPage: PSEPage?

    private let activityIndicator = UIActivityIndicatorView(style: .large)
    private let progressView = UIProgressView(progressViewStyle: .default)
    private let pageLabel = UILabel()

    /// Opens an edition from the catalog, on the page with the given GUID
    /// if you pass one.
    init(published: PSEPublished, openingPageGUID: String? = nil) {
        self.published = published
        self.openingPageGUID = openingPageGUID
        super.init(nibName: nil, bundle: nil)
    }

    /// Shows an edition you've already opened, such as a bookmark's.
    init(source: PSEEditionSource, openingPage: PSEPage? = nil) {
        self.published = source.published
        self.source = source
        self.openingPageGUID = nil
        self.openingPage = openingPage
        super.init(nibName: nil, bundle: nil)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .systemBackground

        hostReader()
        addChrome()

        if let source {
            show(source, at: openingPage)
        } else {
            openEdition()
        }
    }

    // MARK: Hosting the reader

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

    // MARK: Opening the edition

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

    private func stopLoading() {
        activityIndicator.stopAnimating()
        progressView.isHidden = true
    }

    // MARK: Chrome

    private func addChrome() {
        // The publication's name, which the catalog fills in when you pass
        // `publicationName:`. An edition resolved from its GUID alone
        // doesn't have one, so fall back to the edition's name.
        title = published.publicationName.isEmpty ? published.name : published.publicationName

        navigationItem.leftBarButtonItem = UIBarButtonItem(
            systemItem: .close,
            primaryAction: UIAction { [weak self] _ in
                self?.dismiss(animated: true)
            }
        )

        pageLabel.font = .preferredFont(forTextStyle: .footnote)
        toolbarItems = [.flexibleSpace(), UIBarButtonItem(customView: pageLabel), .flexibleSpace()]
        navigationController?.isToolbarHidden = false

        activityIndicator.translatesAutoresizingMaskIntoConstraints = false
        progressView.translatesAutoresizingMaskIntoConstraints = false
        view.addSubview(activityIndicator)
        view.addSubview(progressView)

        NSLayoutConstraint.activate([
            activityIndicator.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            activityIndicator.centerYAnchor.constraint(equalTo: view.centerYAnchor),
            progressView.centerXAnchor.constraint(equalTo: view.centerXAnchor),
            progressView.centerYAnchor.constraint(equalTo: view.centerYAnchor),
            progressView.widthAnchor.constraint(equalToConstant: 200)
        ])
    }

    /// Shows the current page's label.
    private func updateChrome() {
        guard let page = reader.currentPage() else {
            return
        }

        // A friendly label, such as "A3", when the edition has one, and
        // otherwise the page number.
        pageLabel.text = "Page \(page.pageLabel)"
        pageLabel.sizeToFit()
    }
}

// MARK: - Following the reader

extension ReaderScreenViewController: PSEditionReaderViewController.ScrollDelegate {

    func didSettleOn(pageIndex: Int, pagingMode: PSEditionPagingMode) {
        updateChrome()
    }

    func willScrollTo(pageIndex: Int, pagingMode: PSEditionPagingMode, source: Any?) {}

    func pageDragged(
        fromPageIndex fromIndex: Int,
        toPageIndex toIndex: Int,
        fractionComplete: CGFloat,
        pagingMode: PSEditionPagingMode
    ) {}
}

// MARK: - Choosing single or double pages

extension ReaderScreenViewController: PSEditionReaderViewController.LayoutDelegate {

    /// Facing pages side by side on a wide screen, the way classic PDF
    /// editions were printed; one page at a time otherwise.
    func pagingMode(forTraits traits: UITraitCollection, size: CGSize) -> PSEditionPagingMode {
        traits.horizontalSizeClass == .regular && size.width > size.height ? .double : .single
    }
}

extension UIViewController {

    /// Shows an error, with a Retry button when there's something to retry.
    func showAlert(title: String, error: Error, retry: (() -> Void)? = nil) {
        let alert = UIAlertController(title: title, message: error.localizedDescription, preferredStyle: .alert)

        if let retry {
            alert.addAction(UIAlertAction(title: "Retry", style: .default) { _ in retry() })
        }

        alert.addAction(UIAlertAction(title: "OK", style: .cancel))
        present(alert, animated: true)
    }
}
```

The sample’s screen also has a download button, a bookmark button, and
link handling; [Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button),
[Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button), and [Opening Links](/documentation/PSReader/Hosting-the-Reader#Opening-Links) add them.

Each feature guide adds stored properties to this class, a few lines to
`updateChrome()`, and methods in an `extension ReaderScreenViewController`.
Keep those extensions in the same file as the class, since they use its
private members.

## Presenting the Screen

The screen draws its chrome in a navigation bar and a toolbar, so present
it inside a navigation controller. Create it in one of two ways:

- `ReaderScreenViewController(published:openingPageGUID:)` takes a
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished`` from your archive (see <doc://com.pagesuite.PSReader/documentation/PSReader/Fetching-the-Archive>) and
  opens it when the screen loads, on the page with that GUID if you pass
  one.
- `ReaderScreenViewController(source:openingPage:)` shows an edition
  you’ve already opened, such as a bookmark’s or a specific downloaded
  copy (see <doc://com.pagesuite.PSReader/documentation/PSReader/Opening-an-Edition>).

The screen’s title is the publication’s name,
[`publicationName`](/documentation/PSReader/PSEPublished/publicationName). [`FeedEditionService`](/documentation/PSReader/FeedEditionService) fills it in only
when you pass `publicationName:` with the publication GUID, so pass it
wherever you load the catalog. An edition resolved from its GUID alone,
with [`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)), has no
publication name, so a screen opened from a deep link or a search result
shows the edition’s name instead. When you know the publication’s name,
set `publicationName` on the entry before you create the screen.

**UIKit:**

```swift
let screen = ReaderScreenViewController(published: published)
let navigationController = UINavigationController(rootViewController: screen)
navigationController.modalPresentationStyle = .fullScreen
present(navigationController, animated: true)
```

**SwiftUI:**

Wrap the screen and its navigation controller in a
`UIViewControllerRepresentable`, and present it full screen. The
screen’s close button dismisses it.

```swift
import PSReader
import SwiftUI

struct ReaderScreen: UIViewControllerRepresentable {
    let published: PSEPublished

    func makeUIViewController(context: Context) -> UINavigationController {
        UINavigationController(rootViewController: ReaderScreenViewController(published: published))
    }

    func updateUIViewController(_ navigationController: UINavigationController, context: Context) {}
}

struct EditionRow: View {
    let published: PSEPublished
    @State private var isReading = false

    var body: some View {
        Button(published.name) {
            isReading = true
        }
        .fullScreenCover(isPresented: $isReading) {
            ReaderScreen(published: published)
                .ignoresSafeArea()
        }
    }
}
```

The feature guides add to `ReaderScreenViewController`, so they
apply unchanged.

[`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) is always a child of your screen; never
present or push it on its own.

## Opening the Edition

[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) opens the downloaded copy
when there is one and streams the edition otherwise, so the screen needs
no offline logic of its own. The screen shows a spinner until the edition
reports progress, then a progress bar: a streamed edition reports progress
as its opening pages download, and a downloaded one opens without
reporting any. When opening fails, the screen hides both and offers a
retry. Opening has no side effects to undo, so retrying is calling it
again. [Opening an Edition](/documentation/PSReader/Opening-an-Edition) covers the other ways to open an edition,
and what else a loading screen can show.

The screen relies on the call to [`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:)) your
app makes at launch; see [Initialize the SDK](/documentation/PSReader/Getting-Started#Initialize-the-SDK).

Until the edition opens, `source` is `nil`. Code that needs the open
edition unwraps it first:

```swift
guard let source else {
    return
}
```

[`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:))
shows the edition. Opening again replaces the edition on screen.

Two calls refresh an open edition, and both keep the reading position:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/reloadPageContent()`` re-renders the
  loaded pages in place, for example after a text-size change.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/reloadData()`` rebuilds every page from
  the source, for example after your layout delegate’s answer changes.

### Passing the App Configuration

The reader’s `open` also takes your app configuration, the [`PSAppConfig`](/documentation/PSReader/PSAppConfig)
published in the PageSuite portal for your shortcode. Most reader screens
don’t need it: every page renders without it. A few features read it,
though, so pass it if your app has a shortcode and uses any of them:

- **In-article adverts.** The adverts templated article pages show within
  their content come from the configuration’s advertising settings: the
  ad stack, the slot, and the targeting.
- **Third-party advert pages.** The built-in rendering loads them against
  the configuration’s advertising domain, unless your media delegate
  supplies a base URL, and with the ad-stack scripts it lists. See
  <doc://com.pagesuite.PSReader/documentation/PSReader/Handling-Advert-Pages>.
- **Widgets** the configuration adds to templated article pages.

Give the screen a property for it:

```swift
// In ReaderScreenViewController:
var appConfig: PSAppConfig?
```

In `show(_:at:)`, pass it when the reader opens the edition:

```swift
reader.open(edition: source, openingPage: page, application: appConfig)
```

Load the configuration with [`AppConfigService`](/documentation/PSReader/AppConfigService), once, and keep it: each
call fetches it from PageSuite. Then set it on each screen you create:

```swift
// Once, for example at launch. Without it, editions still open.
let appConfig = try? await AppConfigService().configuration(forShortcode: "SHORTCODE")

let screen = ReaderScreenViewController(published: published)
screen.appConfig = appConfig
```

The sample’s demo publications use none of these three features, so its
reader screen leaves the configuration out. If yours might, set it.

The masthead logo some page templates show isn’t on the list: your reader
never reads it from the configuration. The prebuilt reader does, which is
why the sample’s Prebuilt app loads a configuration and shows the demo’s
logo; for your reader screen, see [Showing the Masthead Logo](/documentation/PSReader/Hosting-the-Reader#Showing-the-Masthead-Logo).

### Showing the Masthead Logo

Your reader fills in the masthead logo some page templates show from its
media delegate’s
[`editionLogoURL(for:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/editionLogoURL(for:)).
Without a media delegate, or with the default implementation, it fills in
no logo. To show yours, make the screen the reader’s media delegate, as
[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps) shows, and return the logo’s URL:

```swift
// In your PSEditionReaderViewController.MediaDelegate extension:
func editionLogoURL(for page: PSEPage) -> String? {
    "https://example.com/logo.png"
}
```

The reader asks for the logo each time it renders a templated page. To
use a dark logo in dark mode, check the screen’s `traitCollection` there. Setting a
media delegate also changes how embeds render; read the overview of
[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps) first.

## Following the Reader

The reader’s [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) tells the
screen when the reader settles on a page, and the screen’s `didSettleOn`
calls `updateChrome()`. Every feature guide adds a few lines to
`updateChrome()` to keep its button in step with the page, so the class
conforms to the scroll delegate once, here, and no guide conforms again.

Read the settled content back through the reader’s current-state queries:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/currentPage()`` is the settled spread’s
  reference page. In double-page mode that’s the page that best represents
  the spread: editorial content wins over an advert beside it.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/currentPageSpread()`` returns the whole
  spread and the paging mode it was built for.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/currentPageIndex()`` is a page-level
  index into the edition’s `pages`.

The delegate’s own indices are *spread* indices for the active
[`PSEditionPagingMode`](/documentation/PSReader/PSEditionPagingMode): in double-page mode one index covers two facing
pages. [The Edition Model](/documentation/PSReader/The-Edition-Model) explains spreads and friendly page labels
such as “A3”; to label both pages of a spread, see
[Labeling Spreads](/documentation/PSReader/Hosting-the-Reader#Labeling-Spreads).

`pageDragged` reports an interactive swipe’s progress from 0 to 1, which
suits a progress bar. `didZoom` reports the end of a pinch on a PDF page
and is optional.

### Reporting Page Views

Report page views from the settled page, too. [Reporting Page Views](/documentation/PSReader/Reporting-Analytics#Reporting-Page-Views)
classifies pages the way the prebuilt UI’s analytics events do and
explains when a settle counts as a view.

## Choosing Single or Double Pages

The screen’s [`PSEditionReaderViewController.LayoutDelegate`](/documentation/PSReader/PSEditionReaderViewController/LayoutDelegate-swift.protocol) shows facing
pages side by side on a wide screen in landscape, such as an iPad, and
one page at a time otherwise. The reader asks again on rotation and
window resizes; without a layout delegate it stays single-page.

Double-page spreads apply to classic PDF editions, which pair facing
pages the way they were printed. Responsive editions and article pages
show one page at a time whatever the delegate returns.

PDF pages fit the viewport according to
[`pdfLayoutMode`](/documentation/PSReader/PSEditionReaderViewController/pdfLayoutMode):
[`PSPDFLayoutMode.fitToWidth`](/documentation/PSReader/PSPDFLayoutMode/fitToWidth) (the default) fills the width and scrolls
down the page; [`PSPDFLayoutMode.fitToHeight`](/documentation/PSReader/PSPDFLayoutMode/fitToHeight) fits the whole page on
screen. Changing it applies to the pages on screen immediately.

## Swift 6 Language Mode

The reader’s delegate protocols aren’t isolated to the main actor yet, so
in the Swift 6 language mode the compiler rejects a view controller’s
conformance: “conformance … crosses into main actor-isolated code”. Mark
the conformance `@preconcurrency`:

```swift
extension ReaderScreenViewController: @preconcurrency PSEditionReaderViewController.ScrollDelegate {
```

The reader calls its delegates on the main thread, so the runtime check
that `@preconcurrency` adds always passes. The same fix applies to every
other reader delegate, and to [`PSEDownloadObserver`](/documentation/PSReader/PSEDownloadObserver) and
[`PSEBookmarkObserver`](/documentation/PSReader/PSEBookmarkObserver).

Add `@preconcurrency` only in the Swift 6 language mode. The Swift 5
language mode accepts the conformances as they are, and warns that the
attribute has no effect.

## Navigating

Programmatic navigation goes through the `scrollTo` family: by spread index
([`scrollTo(index:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(index:source:))), to the front,
or to a page, article, or section, either as a model object or by GUID.
Each call takes an optional `source` token that the reader hands back,
untouched, to `willScrollTo`. Tag your own navigation with any value you
like, and you can tell it apart from user swipes, which report `nil`:

```swift
struct ContentsJump {}

reader.scrollTo(page: page, source: ContentsJump())
```

Then, in the screen’s `willScrollTo(pageIndex:pagingMode:source:)`, check
for it:

```swift
let fromContents = source is ContentsJump
```

The reader tags its own navigation too: a link or hotspot inside a page
reports a [`PageJumpNavigationSource`](/documentation/PSReader/PageJumpNavigationSource), [`ArticleJumpNavigationSource`](/documentation/PSReader/ArticleJumpNavigationSource),
or [`SectionJumpNavigationSource`](/documentation/PSReader/SectionJumpNavigationSource), and restoring the position after
`reloadData()` reports a [`ReloadDataNavigationSource`](/documentation/PSReader/ReloadDataNavigationSource).

## Building the Chrome

The reader reports what the rest of your chrome needs. Drive it from
`updateChrome()`:

- **Text size.** Offer a text-size control only on pages whose
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/hasResizableText`` is `true`; see <doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader#Article-Text-Size>.
- **Bookmark button.** Enable it only when the page on screen has
  something to bookmark. <doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Bookmark-Button> builds it.
- **Download button.** <doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Download-Button> builds one that
  follows the edition’s download.
- **Share and print.** <doc://com.pagesuite.PSReader/documentation/PSReader/Adding-a-Share-Button> builds a share button,
  and covers printing.
- **Page label.** Label the page on screen, or both pages of a spread; see
  <doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader#Labeling-Spreads>.

### Labeling Spreads

[`pageLabel`](/documentation/PSReader/PSEPage/pageLabel) is the publisher’s label for a page, such as “A2”,
when the edition has one, and the page number otherwise;
[Friendly Page Labels](/documentation/PSReader/The-Edition-Model#Friendly-Page-Labels) explains where labels come
from. In double-page mode a spread shows two pages, so label the spread
from its pages, leaving out advert pages, which have no printed label:

```swift
extension ReaderScreenViewController {

    /// "Page A2–A3" for a spread, "Page A1" for a single page, or `nil`
    /// for a spread of adverts only.
    func pageTitle(for spread: PSEPageSpread) -> String? {
        let labels = spread.nonAdvertPages().map(\.pageLabel)
        guard !labels.isEmpty else {
            return nil
        }

        return "Page " + labels.joined(separator: "–")
    }
}
```

Then, at the end of `updateChrome()`, add:

```swift
// Label the whole spread, such as "Page A2–A3". This replaces the
// text of the single page's label set above.
if let (spread, _) = reader.currentPageSpread() {
    pageLabel.text = pageTitle(for: spread) ?? "Advertisement"
    pageLabel.sizeToFit()
}
```

Keep the earlier line that labels the single page: this block replaces
its text whenever the reader reports a spread, and removing it can leave
`page` unused. Don’t parse labels, which are free text such as “Sport 4”
or “iv”; to sort or compare pages, use their order in
[`pages`](/documentation/PSReader/PSEEdition/pages). “Page” and “Advertisement” are your chrome’s text,
so translate them with the rest of your strings.

### Going Back After a Jump

When a link inside a page jumps to an article or another page, the
prebuilt reader offers a way back. The jump’s token carries the page it
started from. Add a button and the page to return to:

```swift
// In ReaderScreenViewController:
private var returnPage: PSEPage?
private lazy var backButton = UIBarButtonItem(
    image: UIImage(systemName: "arrow.uturn.backward"),
    style: .plain,
    target: self,
    action: #selector(goBack)
)
```

In `addChrome()`, add it to the toolbar, disabled until a jump:

```swift
backButton.isEnabled = false
toolbarItems?.insert(backButton, at: 0)
```

Fill in the screen’s `willScrollTo(pageIndex:pagingMode:source:)`, so it
remembers the starting page of a jump and forgets it on any other move:

```swift
func willScrollTo(pageIndex: Int, pagingMode: PSEditionPagingMode, source: Any?) {
    switch source {
    case let jump as ArticleJumpNavigationSource:
        returnPage = jump.sourcePage
    case let jump as PageJumpNavigationSource:
        returnPage = jump.sourcePage
    case is ReloadDataNavigationSource:
        break
    default:
        returnPage = nil
    }

    backButton.isEnabled = returnPage != nil
}
```

And go back when the user taps the button:

```swift
extension ReaderScreenViewController {

    @objc func goBack() {
        if let returnPage {
            reader.scrollTo(page: returnPage)
        }
    }
}
```

### Opening Links

The reader opens `mailto:` links itself and hands most others to your
app: it posts [`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification)
app-wide, with the `URL` under
[`linkTappedURLKey`](/documentation/PSReader/PSEditionReaderViewController/linkTappedURLKey). Without an observer,
those links do nothing. The sample observes the notification while its
reader screen is on screen, and opens web links in an
`SFSafariViewController` and every other scheme, such as `tel:`, through
the system, since a Safari view controller takes only web URLs; its code
is in [Open Links](/documentation/PSReader/Building-a-Reader-App#Open-Links).
[Opening Links](/documentation/PSReader/Handling-Media-and-Link-Taps#Opening-Links) lists which links reach
the observer.

## Collapsing Chrome on Scroll

Chrome can float over the pages instead of sitting between bars: pin the
reader’s view to the screen’s edges, put your own bar over it (`topBar`
below), and attach a [`PSEScrollCollapseController`](/documentation/PSReader/PSEScrollCollapseController). It hides the bar as
the user scrolls down a page and brings it back as they scroll up. Register
the bar’s animation on it and attach it to the reader, which feeds it
scroll activity from every page:

```swift
let collapse = PSEScrollCollapseController()
collapse.addAnimation(id: self) { [weak self] state in
    guard let self else { return }
    topBar.transform = state == .collapsed
        ? CGAffineTransform(translationX: 0, y: -topBar.frame.maxY)
        : .identity
}
reader.scrollCollapseController = collapse
```

Each block runs inside the controller’s animator, and drags scrub the
transition interactively. Zooming into a PDF page also collapses the
chrome, and zooming back out reveals it. To reveal the chrome when the
page changes, as the prebuilt reader does, add this to `updateChrome()`:

```swift
reader.scrollCollapseController?.showIfNeeded()
```

To fade or move other views in step with the chrome, read
[`onCollapseProgress`](/documentation/PSReader/PSEScrollCollapseController/onCollapseProgress), which reports progress
from 0 (expanded) to 1 (collapsed) on every frame that changes it. Set
[`collapseEngagementDistance`](/documentation/PSReader/PSEScrollCollapseController/collapseEngagementDistance) to let short
scrolls pass before the chrome starts to collapse.

## Article Text Size

[`PSEArticleTextSize`](/documentation/PSReader/PSEArticleTextSize) is the user’s text size for templated article
pages. It’s global and persists across launches. Apply a change by
re-rendering the pages:

```swift
PSEArticleTextSize.current = .large
reader.reloadPageContent()
```

Offer the control only when the current page’s
[`hasResizableText`](/documentation/PSReader/PSEPage/hasResizableText) is `true`; PDF, web, and advert pages don’t
respond.

Your settings screen’s other reading preferences map onto the reader the
same way. PDF fit is [`pdfLayoutMode`](/documentation/PSReader/PSEditionReaderViewController/pdfLayoutMode).
Single or double pages is your layout delegate’s answer, applied with
[`reloadData()`](/documentation/PSReader/PSEditionReaderViewController/reloadData()). For a “download on Wi-Fi
only” preference, see
[Connectivity and Background Behavior](/documentation/PSReader/Adding-a-Download-Button#Connectivity-and-Background-Behavior). To
reopen an edition where the user stopped reading, see
[Resuming Where the User Left Off](/documentation/PSReader/Opening-an-Edition#Resuming-Where-the-User-Left-Off).

## Localizing the Reader’s Text

Your chrome is your own to localize. Inside the pages, the reader draws
a little text of its own:

- **Comment buttons** in article pages, when you set a commenting
  delegate: “Comment”, “View comments”, and their counts.
- **Embed placeholders**, “Tap to open embed”, on third-party embeds in
  article pages.
- **The failed-page view**, “Failed to load page” and “Tap to retry”,
  over a page whose content didn’t load.

The reader takes these strings from [`LocalizationManager`](/documentation/PSReader/LocalizationManager), the same as
the prebuilt UI, so a translation in your app’s `Localizable` strings, or
a manager subclass, changes them; see [Localization](/documentation/PSReader/Localization). To replace the
failed-page view itself, see [Other Delegates](/documentation/PSReader/Hosting-the-Reader#Other-Delegates).

Advert pages are the exception. The reader’s built-in advert rendering
labels fixed-size slots “Advertisement”, in English, whatever your strings
say; to show your own label, see
[Localizing the Advertisement Label](/documentation/PSReader/Handling-Advert-Pages#Localizing-the-Advertisement-Label).

## Other Delegates

The reader has four more delegates, all optional. Set each in
`hostReader()`, beside the scroll and layout delegates, with one line such
as `reader.mediaDelegate = self`:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol`` handles media hotspots,
  galleries, and third-party embeds. See <doc://com.pagesuite.PSReader/documentation/PSReader/Handling-Media-and-Link-Taps>.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol`` places a comment
  button in article pages and routes its taps to you. See
  <doc://com.pagesuite.PSReader/documentation/PSReader/Adding-Comment-Buttons>.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol`` renders advert pages
  with your own ad stack. See <doc://com.pagesuite.PSReader/documentation/PSReader/Handling-Advert-Pages>.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/ErrorDelegate-swift.protocol`` supplies the view shown
  over a page that failed to load; tapping it retries the page.
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionErrorView`` is the standard look, with your own strings:
  
  ```swift
  extension ReaderScreenViewController: PSEditionReaderViewController.ErrorDelegate {
  
      func genericErrorView() -> UIView {
          PSEditionErrorView(
              messageText: String(localized: "This page didn't load."),
              tapToRetryText: String(localized: "Tap to try again")
          )
      }
  }
  ```

## Topics

### The Reader

[`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController)

A view controller that presents an edition from PageSuite’s current
system, classic PDF or responsive, as a horizontally paged reader.

### Layout

[`PSEditionPagingMode`](/documentation/PSReader/PSEditionPagingMode)

How many pages the reader lays out per spread.

[`PSPDFLayoutMode`](/documentation/PSReader/PSPDFLayoutMode)

How the reader fits PDF pages inside the viewport.

### Navigating

[`ArticleJumpNavigationSource`](/documentation/PSReader/ArticleJumpNavigationSource)

The scroll-source token the reader passes when in-page content triggers
a jump to an article.

[`PageJumpNavigationSource`](/documentation/PSReader/PageJumpNavigationSource)

The scroll-source token the reader passes when a media overlay or link
triggers a jump to a page.

[`SectionJumpNavigationSource`](/documentation/PSReader/SectionJumpNavigationSource)

The scroll-source token the reader passes when in-page content (a
section link or media hotspot) triggers a jump to a section.

[`ReloadDataNavigationSource`](/documentation/PSReader/ReloadDataNavigationSource)

The scroll-source token the reader passes when restoring position after
a data reload.

### Collapsing Chrome on Scroll

[`PSEScrollCollapseController`](/documentation/PSReader/PSEScrollCollapseController)

Drives collapse-on-scroll chrome (navigation bars, toolbars) from one or
more scroll views.

### Article Text Size

[`PSEArticleTextSize`](/documentation/PSReader/PSEArticleTextSize)

The user-selectable text size for templated article pages.

### Errors

[`PSEditionErrorView`](/documentation/PSReader/PSEditionErrorView)

The standard page-failure view: a message with a tap-to-retry hint.

