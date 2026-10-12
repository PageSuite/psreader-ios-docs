<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Analytics",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Analytics"
}
-->

# Analytics

Forward what users open, view, save, and search in the prebuilt UI to
your analytics provider.

## Overview

The prebuilt UI reports what the user does as analytics events: edition
launches, page views, shares, downloads, bookmarks, searches, and carousel
navigation. [`EventChannel`](/documentation/PSReader/EventChannel) delivers them to the subscribers you
register; sending them on to an analytics provider is up to you.
Building a custom UI? See [Reporting Analytics](/documentation/PSReader/Reporting-Analytics).

Each event is a case of [`EventChannel.AnalyticsEvent`](/documentation/PSReader/EventChannel/AnalyticsEvent) that carries a
context describing it. Subscribe at launch, before you show any SDK
screen:

```swift
import PSReader

final class AnalyticsForwarder: EventSubscriber {

    func analytics(event: EventChannel.AnalyticsEvent) {
        switch event {
        case .feedEditionLaunch(let context):
            print("Opened", context.published?.name ?? "an edition")
        default:
            break
        }
    }
}

// At launch, before you show any SDK screen:
let analytics = AnalyticsForwarder()   // keep a strong reference
EventChannel.shared.subscribe(analytics)
```

## Subscribing and Delivery

[`shared`](/documentation/PSReader/EventChannel/shared) holds its subscribers weakly, so keep a strong
reference to yours, for example as a property of your app delegate. A
subscriber that’s deallocated stops receiving events; you don’t need to
unsubscribe. Call [`unsubscribe(_:)`](/documentation/PSReader/EventChannel/unsubscribe(_:)) to stop delivery
sooner.

Call [`subscribe(_:)`](/documentation/PSReader/EventChannel/subscribe(_:)) and `unsubscribe(_:)` on the main
thread. Events arrive on the main thread too, asynchronously, just after
the action that caused them. Every subscriber receives every event, and
subscribing the same object twice delivers each event to it twice.

Nothing is replayed: a subscriber receives the events that happen after it
subscribes. Subscribe at launch, before you show any SDK screen, so the
first launch and page view aren’t missed.

You can’t post events yourself: posting is internal to the SDK, and the
contexts have no public initializers. Report anything else, such as
activity in screens of your own, to your provider directly.

## Mapping Events to Your Provider

Route every event through one reporting function, named after the
prebuilt UI’s events. If your app mixes in screens of your own, they call
the same function (see [Reporting Analytics](/documentation/PSReader/Reporting-Analytics)), so the app reports one
vocabulary:

```swift
import PSReader

/// Your one reporting function: the forwarder routes the prebuilt UI's
/// events here, and a custom reader screen calls it directly.
enum ReaderAnalytics {

    static func track(_ name: String,
                      published: PSEPublished? = nil,
                      page: PSEPage? = nil,
                      properties: [String: Any] = [:]) {
        var properties = properties
        if let published {
            properties["publication"] = published.applicationGUID.isEmpty
                ? published.publicationGUID
                : published.applicationGUID
            properties["edition"] = published.editionGUID
            properties["editionName"] = published.name
        }
        if let page {
            properties["page"] = page.pageLabel
        }
        // Send `name` and `properties` to your analytics provider.
    }
}

final class AnalyticsForwarder: EventSubscriber {

    func analytics(event: EventChannel.AnalyticsEvent) {
        switch event {
        case .carouselView(let context):
            ReaderAnalytics.track("carouselView", properties: ["section": context.sectionName])

        case .feedEditionLaunch(let context):
            track("feedEditionLaunch", context)
        case .feedEditionSectionView(let context):
            track("feedEditionSectionView", context)
        case .feedEditionArticleView(let context):
            track("feedEditionArticleView", context)
        case .feedEditionReplicaView(let context):
            track("feedEditionReplicaView", context)
        case .feedEditionOtherPageView(let context):
            track("feedEditionOtherPageView", context)
        case .feedEditionShare(let context):
            track("feedEditionShare", context)

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

        case .searchCompleted(let context):
            ReaderAnalytics.track("searchCompleted", properties: [
                "query": context.query,
                "results": context.totalCount,
            ])
        case .searchResultTapped(let result, let context):
            ReaderAnalytics.track("searchResultTapped", properties: [
                "query": context.query,
                "headline": result.headline ?? "",
            ])

        default:
            break
        }
    }

    private func track(_ name: String, _ context: EventChannel.FeedEditionEventContext) {
        ReaderAnalytics.track(name, published: context.published,
                              page: context.pageSpread?.referencePage())
    }
}
```

In the prebuilt UI’s events, [`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID) holds the
publication GUID. The fallback to [`publicationGUID`](/documentation/PSReader/PSEPublished/publicationGUID) serves
custom screens, where an edition resolved from its edition GUID alone
leaves it empty.

> Replica: Add replica editions’ events to the same `switch`, reading page
> numbers from their contexts:
> 
> ```swift
> case .replicaPageView(let context):
>     ReaderAnalytics.track("replicaPageView", properties: ["page": context.pageNumber ?? 0])
> ```

## Where Events Come From

Each prebuilt screen reports what happens on it and in the reader it
opens:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController`` reports `carouselView` each time a section
  or subsection comes into view. Its archive, bookmarks, downloads, and
  search sections report as the screens below do.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController`` reports `feedEditionLaunch` once the
  edition opens, a page view each time a page settles, and
  `feedEditionShare` from its share button.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController`` and ``doc://com.pagesuite.PSReader/documentation/PSReader/DownloadsViewController`` report
  nothing themselves; the reader they open reports as above.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksViewController`` opens bookmarks in the same reader. A
  bookmark opened offline, from an edition that isn’t downloaded, opens
  in a reader of saved bookmarks instead, which reports
  `feedEditionBookmarkView` and `feedEditionShareBookmark`.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchViewController`` reports `searchCompleted` and
  `searchResultTapped`, then the reader’s events for the result the user
  opens.

Downloads and bookmarks are reported whatever makes the change, a screen
or your own code: [`EventChannel`](/documentation/PSReader/EventChannel) observes [`PSEDownloadManager`](/documentation/PSReader/PSEDownloadManager) and
[`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager) itself. `carouselView` comes only from the
carousel.

> Replica: Replica editions report `replica…` events in place of the
> `feedEdition…` ones, with ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/ReplicaEventContext`` and
> ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/ReplicaArticleEventContext`` as their contexts. In
> replica editions the reader also reports content-browser navigation,
> link taps, printing, and article text-size changes, which have no
> equivalent on the current system. Carousel and search events are the same for both systems.
> To find out which system a publication is on, see
> <doc://com.pagesuite.PSReader/documentation/PSReader/Edition-Platforms>.

## Event Categories

Every event is a case of [`EventChannel.AnalyticsEvent`](/documentation/PSReader/EventChannel/AnalyticsEvent), whose page lists
them all. Editions on PageSuite’s current system report the events
below.

### Carousel Navigation

[`EventChannel.AnalyticsEvent.carouselView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/carouselView(_:)) fires when the carousel
first appears and whenever another section or subsection comes into view.
Its [`EventChannel.CarouselEventContext`](/documentation/PSReader/EventChannel/CarouselEventContext) gives the section’s index and
name, the subsection’s index and name (`subsectionName` is `nil` for a
section without subsections), and a
[`contentType`](/documentation/PSReader/EventChannel/CarouselEventContext/contentType-swift.property) saying
what the section shows: an archive or kiosk, with its publication GUIDs,
bookmarks, downloads, or search.

A dynamic archive reports `dynamicArchive(shortCode:)` while its
configuration loads. If it’s still on screen once loaded, it reports again
with its resolved type.

> Replica: Replica sections report `replicaArchive(guid:)` and
> `replicaPublicationKiosk(guids:)`, with replica publication GUIDs.

### Opening Editions

[`EventChannel.AnalyticsEvent.feedEditionLaunch(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionLaunch(_:)) fires each time the
prebuilt reader opens an edition, whichever screen opened it. Its
context’s `pageSpread` holds the page the reader opened on: the page you
asked for, otherwise the page the user last viewed, otherwise the first
page. That page also reports a page view.

> Replica: Replica editions report `replicaLaunch(_:)`. Its context’s
> `pageNumber` is set only when the reader was asked to open on a
> specific page.

### Page Views

The prebuilt reader reports a page view each time a spread settles on
screen, classified by the type of the spread’s reference page
([`referencePage()`](/documentation/PSReader/PSEPageSpread/referencePage()), which prefers editorial content over
an advert beside it):

- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionSectionView(_:)``: a section
  front (`templateSection`).
- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionArticleView(_:)``: an article
  page (`templateArticle`).
- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionReplicaView(_:)``: a PDF page
  (``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/isPDF``), such as a page of a classic PDF edition. “Replica”
  in its name means the classic PDF look, not the legacy system; see
  <doc://com.pagesuite.PSReader/documentation/PSReader/Edition-Platforms>.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionOtherPageView(_:)``: any other
  page, such as a web page or an advert page.

A spread settles more often than the user turns to a new one, after a
swipe that springs back to the same page for example, so skip a report
whose spread matches the previous one to count distinct page views.
[Reporting Analytics](/documentation/PSReader/Reporting-Analytics) lists when a spread settles.

The reader of saved bookmarks that [`BookmarksViewController`](/documentation/PSReader/BookmarksViewController) opens
offline reports [`EventChannel.AnalyticsEvent.feedEditionBookmarkView(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionBookmarkView(_:))
for each bookmark it shows, with the [`PSEBookmark`](/documentation/PSReader/PSEBookmark), instead of these.

> Replica: Replica editions report `replicaPageView(_:)`, whose context
> gives the page number and, for a double-page spread, `leftPageNumber`
> and `rightPageNumber`. An article shown in the reader reports
> `replicaArticleView(_:)`, and tapping an article on a page reports
> `replicaArticleTapped(_:)`.

### Downloads

[`EventChannel.AnalyticsEvent.feedEditionDownloaded(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionDownloaded(_:)) fires when an
edition’s download completes, and
[`EventChannel.AnalyticsEvent.feedEditionDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionDeleted(_:)) when a stored copy
is removed: by the user, by your code, or by the prebuilt archive
discarding a copy that’s out of date. Both carry the edition’s
[`PSEPublished`](/documentation/PSReader/PSEPublished).

Each edition that [`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:))
adds also reports `feedEditionDownloaded`, if you’ve subscribed by then.

> Replica: `replicaDownloaded(_:)` and `replicaDeleted(_:)` report replica
> editions, carrying the legacy `PSEdition`.

### Bookmarks

[`EventChannel.AnalyticsEvent.feedEditionArticleBookmark(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionArticleBookmark(_:)) and
[`EventChannel.AnalyticsEvent.feedEditionArticleBookmarkDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionArticleBookmarkDeleted(_:))
carry the [`PSEBookmarkArticle`](/documentation/PSReader/PSEBookmarkArticle);
[`EventChannel.AnalyticsEvent.feedEditionPageBookmark(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionPageBookmark(_:)) and
[`EventChannel.AnalyticsEvent.feedEditionPageBookmarkDeleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionPageBookmarkDeleted(_:)) carry
the [`PSEBookmarkPage`](/documentation/PSReader/PSEBookmarkPage). They fire for every change made through
[`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager), from any screen or from your code. The prebuilt
reader’s bookmark button bookmarks each page of a double-page spread, so
it reports one event per page.

Each page bookmark that
[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)) adds also
reports `feedEditionPageBookmark`, if you’ve subscribed by then.

> Replica: `replicaPageBookmark(_:)`, `replicaArticleBookmark(_:)`, and
> their `…Deleted` twins report replica bookmarks, carrying the legacy
> `PSBookmark` and `PSBookmarkArticle`.

### Sharing

[`EventChannel.AnalyticsEvent.feedEditionShare(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionShare(_:)) fires when the user
taps the prebuilt reader’s share button, just before the share sheet
appears. It isn’t sent when your [`ShareDelegate`](/documentation/PSReader/ShareDelegate) returns no share
context, and it doesn’t tell you whether the user went on to share.
[`EventChannel.AnalyticsEvent.feedEditionShareBookmark(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionShareBookmark(_:)) is its twin
in the offline reader of saved bookmarks, carrying the [`PSEBookmark`](/documentation/PSReader/PSEBookmark).

> Replica: `replicaPageShare(_:)` and `replicaArticlePageShare(_:)` report
> shares in replica editions, and `replicaPagePrint(_:)` and
> `replicaArticlePagePrint(_:)` report printing.

### Search

[`EventChannel.AnalyticsEvent.searchCompleted(_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/searchCompleted(_:)) fires when a search
returns its first page of results, including an empty one. Loading more
results and failed searches send nothing.
[`EventChannel.AnalyticsEvent.searchResultTapped(_:_:)`](/documentation/PSReader/EventChannel/AnalyticsEvent/searchResultTapped(_:_:)) fires when the
user taps a result, with the [`SearchResult`](/documentation/PSReader/SearchResult).

## Context Objects

Most events carry a context; the rest carry a model directly.

- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/FeedEditionEventContext`` comes with launches, page
  views, and shares. Its ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/FeedEditionEventContext/published``,
  ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/FeedEditionEventContext/edition``, and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/FeedEditionEventContext/pageSpread`` are optional. Read
  the page the event is about with `pageSpread?.referencePage()`. Identify
  the edition by its ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/editionGUID`` and the publication by
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/applicationGUID``, which holds the publication GUID.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/CarouselEventContext`` comes with `carouselView`.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/SearchEventContext`` comes with both search events: the
  query, the ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchType`` filter, the total result count, and the
  publications searched (the one the user filtered to, otherwise all of
  them).
- Download events carry the ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished``. Bookmark events carry the
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkArticle`` or ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkPage``, and the offline bookmark
  reader’s events the ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmark``.

> Replica: ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/ReplicaEventContext`` carries the edition and
> page numbers, and ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/ReplicaArticleEventContext`` the edition
> and article. Their `edition` and `article` are legacy model types
> (`PSEdition`, `PSArticle`).

> Tip: Keep a `default` case in your `switch` over
> ``doc://com.pagesuite.PSReader/documentation/PSReader/EventChannel/AnalyticsEvent``. A new SDK version can add events, and
> the `default` case keeps your code compiling when it does.

## Topics

### Subscribing

[`EventChannel`](/documentation/PSReader/EventChannel)

Singleton class responsible for analytics reporting.

[`EventSubscriber`](/documentation/PSReader/EventSubscriber)

A type that listens to analytics events broadcast from an `EventChannel`.

