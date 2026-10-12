<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Reporting-Analytics",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Reporting Analytics"
}
-->

# Reporting Analytics

Report what the user opens, views, saves, and shares in your own screens to your analytics provider.

## Overview

The prebuilt UI reports what the user does as events on [`EventChannel`](/documentation/PSReader/EventChannel).
The core reader reports nothing: [`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) never
posts an event, so a custom UI reports its own activity, from the
delegates and notifications through which the reader tells you what
happened. Downloads and bookmarks are the exception; their events still
arrive (see [Downloads and Bookmarks](/documentation/PSReader/Reporting-Analytics#Downloads-and-Bookmarks)).

Using the prebuilt UI? See [Analytics](/documentation/PSReader/Analytics).

Send everything through one reporting function of your own:

```swift
import PSReader

/// Your one reporting function.
enum ReaderAnalytics {

    /// Reports an event, with the edition's identifiers when you pass one.
    ///
    /// Pass `publicationGUID` for an edition you resolved from an edition
    /// GUID, such as a search result's or a link's.
    static func track(_ name: String,
                      published: PSEPublished? = nil,
                      publicationGUID: String? = nil,
                      page: PSEPage? = nil,
                      properties: [String: Any] = [:]) {
        var properties = properties

        if let published {
            // applicationGUID holds the publication GUID, but it's empty on
            // an edition resolved from an edition GUID.
            let publication = published.applicationGUID.isEmpty ? publicationGUID : published.applicationGUID

            // Last resort: the backend's filing GUID, which can differ.
            properties["publication"] = publication ?? published.publicationGUID
            properties["edition"] = published.editionGUID
            properties["editionName"] = published.name
        }

        if let page {
            properties["page"] = page.pageLabel
        }

        // Send `name` and `properties` to your analytics provider.
    }
}
```

[`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID) holds the publication GUID for every
edition you list from the catalog. It’s empty on an edition resolved with
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)), so for those, pass the
publication GUID you resolved it with: a search result’s
[`applicationId`](/documentation/PSReader/SearchResult/applicationId), or the GUID your link carries.
[`publicationGUID`](/documentation/PSReader/PSEPublished/publicationGUID) is the backend’s own filing GUID and can
differ from the publication GUID, so the function falls back to it only
when it has nothing else. See [Identifiers](/documentation/PSReader/Identifiers).

## Choosing Event Names

The event names on this page are the prebuilt UI’s. If your app mixes
prebuilt screens with your own, use them for your custom screens too, and
route the prebuilt events into the same function with the forwarder in
[Mapping Events to Your Provider](/documentation/PSReader/Analytics#Mapping-Events-to-Your-Provider). Both sides then feed one
report: an edition opened in your reader and one opened in the prebuilt
reader both count as `feedEditionLaunch`. An app that’s custom throughout
can name its events however it likes.

The prebuilt names keep the SDK’s historic wording: the `feedEdition…`
events cover every edition on PageSuite’s current system, and
`feedEditionReplicaView` reports a PDF page. [Edition Platforms](/documentation/PSReader/Edition-Platforms)
explains the names.

## Where Each Event Comes From

Each prebuilt event has a source in a custom UI:

|Prebuilt event                                                                                          |Report it from                                                                                                |
|--------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
|`carouselView`                                                                                          |Your own navigation, as each screen of your archive appears.                                                  |
|`feedEditionLaunch`                                                                                     |Your reader screen, when it opens the edition.                                                                |
|`feedEditionSectionView`, `feedEditionArticleView`, `feedEditionReplicaView`, `feedEditionOtherPageView`|Your reader screen, each time the reader settles on a page.                                                   |
|`feedEditionBookmarkView`                                                                               |The same, when the reader shows a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarksEdition``.|
|`feedEditionShare`, `feedEditionShareBookmark`                                                          |Your share button.                                                                                            |
|`feedEditionDownloaded`, `feedEditionDeleted`                                                           |``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel``, which still reports them.               |
|`feedEditionArticleBookmark`, `feedEditionPageBookmark`, and their `…Deleted` twins                     |``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel``, which still reports them.               |
|`searchCompleted`, `searchResultTapped`                                                                 |Your search screen.                                                                                           |

The reader also tells you about taps the prebuilt reader doesn’t
report, so their names are yours: links through
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification), and media
through the reader’s [`PSEditionReaderViewController.MediaDelegate`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol) (see
[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps)).

## Reporting From Your Reader Screen

Most events come from `ReaderScreenViewController`, the reader screen
from [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader). Give it a property for the publication
GUID of an edition resolved from an edition GUID:

```swift
var publicationGUID: String?
```

Set it wherever you open such an edition, for example when you open a
search result in [Opening a Result](/documentation/PSReader/Building-a-Search-Screen#Opening-a-Result):

```swift
let screen = ReaderScreenViewController(published: published, openingPageGUID: result.pageId)
screen.publicationGUID = result.applicationId
```

Add a helper that reports an event about the open edition, in an
extension in the same file as the class:

```swift
extension ReaderScreenViewController {

    /// Reports an event about the open edition.
    func track(_ name: String, page: PSEPage? = nil, properties: [String: Any] = [:]) {
        guard let source else {
            return
        }
        ReaderAnalytics.track(name, published: source.published, publicationGUID: publicationGUID,
                              page: page, properties: properties)
    }
}
```

Then report the launch as the edition opens, with its opening page. In
`show(_:at:)`, add the highlighted line:

```swift, highlight=[3]
private func show(_ source: PSEEditionSource, at page: PSEPage?) {
    self.source = source
    track("feedEditionLaunch", page: page ?? source.edition.pages?.first)
    reader.open(edition: source, openingPage: page)
    stopLoading()
    updateChrome()
}
```

## Reporting Page Views

The reader tells its [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol)
each time it settles on a page, in `didSettleOn(pageIndex:pagingMode:)`:

- once the opening page is laid out after `open`, so the edition’s first
  page reports itself, as it does in the prebuilt reader;
- after every swipe, whether it turned the page or sprang back to the
  same one;
- at the end of every jump, such as a link to another page or your own
  `scrollTo` call;
- when a rotation or resize changes the paging mode or the spread on
  screen.

Report page views from there, not from `updateChrome()`, which also runs
when your own buttons change something. Add a property that remembers the
page you reported last:

```swift
private var lastReportedPageGUID: String?
```

In `didSettleOn(pageIndex:pagingMode:)`, add the highlighted line:

```swift, highlight=[2]
func didSettleOn(pageIndex: Int, pagingMode: PSEditionPagingMode) {
    reportPageView()
    updateChrome()
}
```

And in the extension, classify the page the way the prebuilt reader does:

```swift
/// Reports the settled page, once per page, by the prebuilt UI's names.
func reportPageView() {
    guard let source, let page = reader.currentPage(), page.pageguid != lastReportedPageGUID else {
        return
    }
    lastReportedPageGUID = page.pageguid

    // Each page of a bookmarks edition comes from its own edition.
    if let saved = source as? PSEBookmarksEdition {
        let bookmark = reader.currentPageIndex().flatMap { index in
            saved.bookmarks.indices.contains(index) ? saved.bookmarks[index] : nil
        }
        ReaderAnalytics.track("feedEditionBookmarkView", published: bookmark?.published, page: page)
        return
    }

    let name: String
    if page.isPDF {
        name = "feedEditionReplicaView"   // Any PDF page, despite the name.
    } else if page.type == "templateSection" {
        name = "feedEditionSectionView"
    } else if page.type == "templateArticle" {
        name = "feedEditionArticleView"
    } else {
        name = "feedEditionOtherPageView"
    }
    track(name, page: page)
}
```

A few choices are yours:

- **Repeats.** The prebuilt reader reports every settle, so a swipe that
  springs back reports the same page again. The `lastReportedPageGUID`
  check skips a page reported last time, which counts distinct page
  views; leave it out to match the prebuilt counts.
- **Spreads.** In double-page mode, ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/currentPage()``
  is the spread’s reference page, which prefers editorial content: a
  spread that pairs an advert with an article reports the article. To
  report both pages, read ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEditionReaderViewController/currentPageSpread()``.
- **Adverts.** An advert page reports `feedEditionOtherPageView`, as it
  does in the prebuilt reader. To leave advert pages out, return early
  when ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/isAdvertPage`` is `true`, and count impressions in your
  advert view controllers instead (see <doc://com.pagesuite.PSReader/documentation/PSReader/Handling-Advert-Pages>).

## Reporting Shares, Searches, and Links

Report a share from your share button’s action. The prebuilt reader
reports one when the user taps the button and it has something to share,
before the share sheet appears; it can’t tell whether the user went on to
share. In `shareTapped()` from [Adding a Share Button](/documentation/PSReader/Adding-a-Share-Button), once the
`guard` has a share context, add:

```swift
track("feedEditionShare", page: page)
```

Report searches from your search screen;
[Reporting Searches](/documentation/PSReader/Building-a-Search-Screen#Reporting-Searches) shows where.

Report link taps from your link observer. In `linkTapped(_:)` from
[Opening Links](/documentation/PSReader/Handling-Media-and-Link-Taps#Opening-Links), once you have the URL,
add:

```swift
track("linkTapped", page: reader.currentPage(), properties: ["url": url.absoluteString])
```

## Downloads and Bookmarks

[`EventChannel`](/documentation/PSReader/EventChannel) observes [`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager) and
[`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager), so it reports the changes your custom UI makes
with the same events the prebuilt UI sends. Subscribe a forwarder for
them at launch:

```swift
final class LibraryAnalytics: EventSubscriber {

    func analytics(event: EventChannel.AnalyticsEvent) {
        switch event {
        case .feedEditionDownloaded(let published):
            ReaderAnalytics.track("feedEditionDownloaded", published: published)
        case .feedEditionDeleted(let published):
            ReaderAnalytics.track("feedEditionDeleted", published: published)
        case .feedEditionArticleBookmark(let bookmark):
            ReaderAnalytics.track("feedEditionArticleBookmark", published: bookmark.published,
                                  properties: ["headline": bookmark.article?.headline ?? ""])
        case .feedEditionPageBookmark(let bookmark):
            ReaderAnalytics.track("feedEditionPageBookmark", published: bookmark.published,
                                  page: bookmark.page)
        default:
            break
        }
    }
}

// At launch:
let libraryAnalytics = LibraryAnalytics()   // Keep a strong reference.
EventChannel.shared.subscribe(libraryAnalytics)
```

The channel holds its subscribers weakly and replays nothing, so keep a
reference and subscribe before the first change; see
[Subscribing and Delivery](/documentation/PSReader/Analytics#Subscribing-and-Delivery). [Downloads](/documentation/PSReader/Analytics#Downloads) and
[Bookmarks](/documentation/PSReader/Analytics#Bookmarks) say when each event fires.

To observe the managers yourself instead, a [`PSEDownloadObserver`](/documentation/PSReader/PSEDownloadObserver) and
a [`PSEBookmarkObserver`](/documentation/PSReader/PSEBookmarkObserver) see the same changes; see
[Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button) and [Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button).