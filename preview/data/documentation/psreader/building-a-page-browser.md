<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Building-a-Page-Browser",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Building a Page Browser"
}
-->

# Building a Page Browser

Give users a thumbnail overview of the edition in your own reader screen,
and jump the reader to the page they tap.

## Overview

A page browser, or contents view, shows the edition at a glance: page
thumbnails labeled the way the publisher prints them. Everything it needs
comes from the open [`PSEEditionSource`](/documentation/PSReader/PSEEditionSource), and a tap jumps the reader. The
same browser serves classic PDF editions, where the thumbnails are the
printed pages, and responsive editions, where they’re section fronts and
article cards. Using the prebuilt reader? Its content browser is built in;
see [The Content Browser](/documentation/PSReader/Customizing-the-Reader-Screen#The-Content-Browser).

This browser lists the edition’s pages, with a thumbnail and label for
each:

```swift
import PSReader
import UIKit

/// The edition's pages, with a thumbnail and the printed label for each.
/// Tapping a page calls `onSelect`.
final class PageBrowserViewController: UITableViewController {

    private let source: PSEEditionSource
    private let pages: [PSEPage]
    private let onSelect: (PSEPage) -> Void

    private var thumbnails: [String: UIImage] = [:]
    private var requested: Set<String> = []

    init(source: PSEEditionSource, onSelect: @escaping (PSEPage) -> Void) {
        self.source = source
        // Advert pages aren't part of the edition's contents.
        self.pages = (source.edition.pages ?? []).filter { !$0.isAdvertPage }
        self.onSelect = onSelect
        super.init(style: .plain)
        title = "Pages"
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "Page")
    }

    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        pages.count
    }

    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let page = pages[indexPath.row]
        let cell = tableView.dequeueReusableCell(withIdentifier: "Page", for: indexPath)

        var content = UIListContentConfiguration.subtitleCell()
        content.text = "Page \(page.pageLabel)"
        content.secondaryText = page.section
        content.image = thumbnail(for: page) ?? UIImage(systemName: "doc")
        content.imageProperties.reservedLayoutSize = CGSize(width: 48, height: 64)
        content.imageProperties.maximumSize = CGSize(width: 48, height: 64)
        cell.contentConfiguration = content

        return cell
    }

    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        onSelect(pages[indexPath.row])
    }

    // MARK: Thumbnails

    /// Returns the page's thumbnail if it's loaded, and otherwise starts
    /// loading it.
    private func thumbnail(for page: PSEPage) -> UIImage? {
        guard let resource = page.effectiveScreenshotURL else {
            return nil
        }

        if requested.insert(resource).inserted {
            loadImage(resource) { [weak self] image in
                self?.thumbnails[resource] = image
                self?.tableView.reloadData()
            }
        }

        return thumbnails[resource]
    }

    /// Loads an absolute URL with URLSession, and an edition resource
    /// through the source, which works for downloaded and streamed
    /// editions alike.
    private func loadImage(_ resource: String, completion: @escaping (UIImage?) -> Void) {
        if resource.hasPrefix("http"), let url = URL(string: resource) {
            URLSession.shared.dataTask(with: url) { data, _, _ in
                DispatchQueue.main.async { completion(data.flatMap(UIImage.init(data:))) }
            }.resume()
        } else if let data = source.resourceManager.cachedData(for: resource) {
            DispatchQueue.main.async { completion(UIImage(data: data)) }
        } else {
            _ = source.resourceManager.dataTask(for: resource) { data in
                DispatchQueue.main.async { completion(data.flatMap(UIImage.init(data:))) }
            }
        }
    }
}
```

Open it from your reader screen, `ReaderScreenViewController` from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader). Add a button to the class:

```swift
// In ReaderScreenViewController:
private lazy var pagesButton = UIBarButtonItem(
    image: UIImage(systemName: "square.grid.2x2"),
    style: .plain,
    target: self,
    action: #selector(showPages)
)
```

In `addChrome()`, add it to the toolbar:

```swift
toolbarItems?.insert(pagesButton, at: 0)
```

And present the browser, jumping the reader to the page the user picks:

```swift
/// Tags the browser's jumps, so the reader screen can tell them from swipes.
struct PageBrowserJump {}

extension ReaderScreenViewController {

    @objc func showPages() {
        guard let source else {
            return
        }

        let browser = PageBrowserViewController(source: source) { [weak self] page in
            self?.dismiss(animated: true)
            self?.reader.scrollTo(page: page, source: PageBrowserJump())
        }
        present(UINavigationController(rootViewController: browser), animated: true)
    }
}
```

The sections below refine it: richer thumbnails, sections, article cards,
and highlighting the pages on screen.

## Thumbnails

[`effectiveScreenshotURL`](/documentation/PSReader/PSEPage/effectiveScreenshotURL) is a page’s thumbnail: its rendered
screenshot when the edition supplies one, and otherwise an image derived
from a PDF page’s content. It’s `nil` for pages with neither.

The reference comes in one of two forms, which `loadImage(_:completion:)`
above handles. Absolute URLs, which screenshots usually are, load with
your app’s usual image loader. Anything else is an edition resource: load
it through the source’s [`resourceManager`](/documentation/PSReader/PSEEditionSource/resourceManager), which reads
it from disk for a downloaded edition, and fetches and caches it for a
streamed one. That keeps one implementation working for every kind of
source.

[`dataTask(for:completion:)`](/documentation/PSReader/PSEEditionResourceManager/dataTask(for:completion:)) returns a
[`PSEDataTask`](/documentation/PSReader/PSEDataTask). In a grid whose cells load their own images, keep it in
the cell and cancel it when the cell is reused, as you would a
`URLSessionDataTask`.

Article cards show the article’s lead image instead.
[`leadAsset()`](/documentation/PSReader/PSEArticle/leadAsset()) picks it: the flagged lead video or image,
else the first image or video, else the article’s landscape image. Each
asset lists candidate URLs; use the first one the resource manager can
resolve:

```swift
func cardImage(for article: PSEArticle, in source: PSEEditionSource) -> String? {
    let candidates: [String]
    switch article.leadAsset() {
    case .image(let image): candidates = image.URLs
    case .video(let video): candidates = video.videoImageURLs
    default:                candidates = []
    }
    return candidates.first { source.resourceManager.resolve(resource: $0) != nil }
}
```

## Labels

Label pages with [`pageLabel`](/documentation/PSReader/PSEPage/pageLabel), as the browser above does: it’s
the publisher’s printed label, such as A1 or B12, where the edition has
one, and the page number otherwise. [Friendly Page Labels](/documentation/PSReader/The-Edition-Model#Friendly-Page-Labels)
explains labels; for a label covering both pages of a spread, see
[Labeling Spreads](/documentation/PSReader/Hosting-the-Reader#Labeling-Spreads).

## Grouping Into Sections

[`pageBrowserSections`](/documentation/PSReader/PSEEdition/pageBrowserSections) is the edition’s own section list for a
browser. Each [`PSEPageBrowserSection`](/documentation/PSReader/PSEPageBrowserSection) has a `title`, a `num`, and a
`color`:

- `num` is the index in ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEdition/pages`` where the section starts. It’s
  an index, not a printed page number.
- `color` is the matching section’s theme color, as a hex string, when the
  edition has one.

Skip entries with empty titles. Some editions number their sections
inconsistently, so check that the starts are in range and increasing, and
otherwise fall back to the pages themselves: walk [`pages`](/documentation/PSReader/PSEEdition/pages) and
start a group whenever [`section`](/documentation/PSReader/PSEPage/section) changes, colored with
[`sectionColor`](/documentation/PSReader/PSEPage/sectionColor). The prebuilt browser does the same.

```swift
struct BrowserSection {
    let title: String
    let color: String?
    var pages: [PSEPage]
}

func browserSections(for edition: PSEEdition) -> [BrowserSection] {
    let pages = edition.pages ?? []
    let starts = (edition.pageBrowserSections ?? []).filter {
        $0.title?.isEmpty == false && pages.indices.contains($0.num)
    }
    let increasing = zip(starts, starts.dropFirst()).allSatisfy { $0.num < $1.num }

    if starts.isEmpty == false, increasing {
        return starts.enumerated().map { index, start in
            let lower = index == 0 ? 0 : start.num
            let upper = index + 1 < starts.count ? starts[index + 1].num : pages.count
            return BrowserSection(title: start.title ?? "", color: start.color,
                                  pages: Array(pages[lower..<upper]))
        }
    }

    var sections: [BrowserSection] = []
    for page in pages {
        if let name = page.section, name != sections.last?.title {
            sections.append(BrowserSection(title: name, color: page.sectionColor, pages: [page]))
        } else if sections.isEmpty == false {
            sections[sections.count - 1].pages.append(page)
        }
    }
    return sections
}
```

Filter advert pages out when you display a section’s pages, not before you
group them, so the section starts still line up with the edition’s pages.

## Pages and Articles

Choose what the browser shows by [`type`](/documentation/PSReader/PSEPage/type) and [`level`](/documentation/PSReader/PSEPage/level):

- **Page thumbnails.** The edition’s pages as laid out: PDF pages
  (`replica_pdf_page`) and web pages (`webview`) in a classic PDF edition,
  and section fronts (`templateSection`) in a responsive one.
- **Article cards.** Pages whose `level` is `article`, one card per page,
  titled with the page’s article headline
  (`page.articles?.first?.headline`) and illustrated with its lead asset.
- **No adverts.** Skip pages whose ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/isAdvertPage`` is `true`.

A classic PDF edition can carry its stories as article pages too. When the
edition has PDF pages ([`isPDF`](/documentation/PSReader/PSEPage/isPDF)) and
[`pagesHaveArticles()`](/documentation/PSReader/PSEEdition/pagesHaveArticles()) is `true`, offer a toggle between pages
and articles, as the prebuilt browser does.

## Navigating and Staying in Sync

The browser jumps with [`scrollTo(page:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(page:source:)).
Its `PageBrowserJump` token reaches the reader screen’s
`willScrollTo(pageIndex:pagingMode:source:)`, so you can tell jumps from
the browser apart from swipes; see [Navigating](/documentation/PSReader/Hosting-the-Reader#Navigating).

To highlight the pages on screen when the browser opens, pass it the
current spread’s pages:

```swift
let onScreen = reader.currentPageSpread()?.0.pages() ?? []
```

A browser that stays visible beside the reader, such as a sidebar on
iPad, updates its highlight from the reader screen’s `updateChrome()`,
which runs whenever the reader settles. The reader reports spread
indices, and double-page mode pairs pages, so go between a page and its
spread with the edition’s helpers; see
[Pages and Spreads](/documentation/PSReader/The-Edition-Model#Pages-and-Spreads).

## Topics

### Sections

[`PSEPageBrowserSection`](/documentation/PSReader/PSEPageBrowserSection)

A section grouping used to build a sectioned page-browser UI.

