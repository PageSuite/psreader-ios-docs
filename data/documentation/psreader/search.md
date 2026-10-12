<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Search",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Search"
}
-->

# Search

Find articles and pages across your publications’ editions with the
prebuilt search screen.

## Overview

The prebuilt search screen runs a full-text query across your
publications’ editions. It has a query field, filters for articles and
pages, and a publication menu when there’s more than one publication.
Tapping a result opens its edition at that page. Building a custom UI?
See [Building a Search Screen](/documentation/PSReader/Building-a-Search-Screen).

Add the screen to the carousel as a section with the `.search(config:)`
content type:

```swift
let searchConfig = SearchConfiguration(globalConfig: globalConfig)

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE"),
        .section(.init(name: "Search", type: .search(config: searchConfig)))
    ]
)
```

![Search results for a query, listing matching articles and pages.](images/com.pagesuite.PSReader/search-results~dark@2x.png)

The carousel searches the publications in all its archive sections,
dynamic or manual, and opens results with each section’s reader
configuration. Editions on PageSuite’s current system that it opens
also get a Search row in the reader’s settings menu, with or without a
search section.

Outside the carousel, search needs a [`SearchDelegate`](/documentation/PSReader/SearchDelegate). It lists the
publications to search, each a [`SearchPublication`](/documentation/PSReader/SearchPublication), and supplies the
reader configuration that opens each one’s results.
[`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate) builds the list from a shortcode’s
configuration, and the carousel brings its own.

## Adding Search to Your Screens

[`SearchViewController`](/documentation/PSReader/SearchViewController) is the carousel’s search screen, for your own
navigation. Give it a search delegate. [`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate)
searches every publication in a shortcode’s archive; it fetches the
shortcode’s configuration the first time a search screen asks, and reuses
it after that:

```swift
let searchDelegate = ApplicationSearchDelegate(
    shortcode: "SHORTCODE",
    readerConfig: ReaderConfiguration(globalConfig: globalConfig)
)

let search = SearchViewController(globalConfig: globalConfig, delegate: searchDelegate)
navigationController?.pushViewController(search, animated: true)
```

To present the screen modally instead, pass `dismissible: true` so it
shows a close button.

If you load the configuration yourself with [`AppConfigService`](/documentation/PSReader/AppConfigService), build
the delegate from it. Set it as [`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig) too,
before you create the screen, so readers opened from results have it for
the features that read it (see
[The App Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration)):

```swift
let appConfig = try await AppConfigService().configuration(forShortcode: "SHORTCODE")
globalConfig.remoteConfig = appConfig

let searchDelegate = ApplicationSearchDelegate(
    application: appConfig,
    readerConfig: ReaderConfiguration(globalConfig: globalConfig)
)
```

## Searching From the Reader

Readers the carousel opens show a Search row in their settings menu.
Readers you open yourself show it only when their reader configuration has
a search delegate. Set one on the configuration you pass to
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController), or on [`readerConfig`](/documentation/PSReader/ArchiveConfiguration/readerConfig),
[`readerConfig`](/documentation/PSReader/BookmarksConfiguration/readerConfig), or
[`readerConfig`](/documentation/PSReader/DownloadsConfiguration/readerConfig):

```swift
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.search?.searchDelegate = ApplicationSearchDelegate(
    shortcode: "SHORTCODE",
    readerConfig: readerConfig
)

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    readerConfig: readerConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

Readers opened from a result keep the row: [`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate)
sets itself as their search delegate when their configuration has none.
Set [`search`](/documentation/PSReader/ReaderConfiguration/search) to `nil` to take search out of the
reader.

## Choosing the Publications

Conform to [`SearchDelegate`](/documentation/PSReader/SearchDelegate) to choose the publications yourself, for
example to search a single title:

```swift
struct DailySearchDelegate: SearchDelegate {
    let readerConfig: ReaderConfiguration

    func searchPublications(completion: @escaping (Result<[SearchPublication], Error>) -> Void) {
        completion(.success([
            SearchPublication(title: "The Daily", guid: "PUBLICATION_GUID")
        ]))
    }

    func searchReaderConfiguration(for publication: SearchPublication) -> ReaderConfiguration? {
        readerConfig
    }
}
```

Pass it to [`SearchViewController`](/documentation/PSReader/SearchViewController), or set it as the
[`searchDelegate`](/documentation/PSReader/SearchConfiguration/searchDelegate) of the carousel’s search section or
of a reader configuration’s [`search`](/documentation/PSReader/ReaderConfiguration/search).

The search screen matches each result to its publication by GUID, so
[`guid`](/documentation/PSReader/SearchPublication/guid) must be the publication GUID. A result whose
publication gets `nil` from
[`searchReaderConfiguration(for:)`](/documentation/PSReader/SearchDelegate/searchReaderConfiguration(for:)) doesn’t open. If
[`searchPublications(completion:)`](/documentation/PSReader/SearchDelegate/searchPublications(completion:)) fails, the screen shows
an error, and tapping it asks the delegate again.
[`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate) fails with [`SearchError.noPublications`](/documentation/PSReader/SearchError/noPublications)
when the shortcode’s configuration lists no publications; a delegate of
your own can report the same error.

> Replica: Replica publications are listed as
> ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchPublicationType/replica``, with their replica publication GUID,
> and searched through ``doc://com.pagesuite.PSReader/documentation/PSReader/ReplicaSearchService``. Results are always pages,
> and each request searches only the first publication passed. Replica
> publications can’t be searched together with publications on the
> current system: the search screen
> chooses its backend from the first publication its delegate lists, and
> the carousel lists its archive sections in order. Give a carousel that
> mixes the two systems a search delegate that lists only one of them.
> 
> Replica results have the type ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/replicaPageType``
> (`"REPLICA_PAGE"`), an ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/editionName`` instead of an edition
> date, and their replica publication GUID in `publicationId` only. The
> search screen opens them in the replica reader;
> ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedReaderViewController`` can’t open them.

## Matching the Search Type

Each publication on PageSuite’s current system is indexed for search
either as an app or as a publication. A request has to name the same type,
[`SearchPublicationType.app`](/documentation/PSReader/SearchPublicationType/app) or [`SearchPublicationType.publication`](/documentation/PSReader/SearchPublicationType/publication), or
that publication returns no results. The two types differ in nothing
else, and `.app` is the default.

- Dynamic archives and ``doc://com.pagesuite.PSReader/documentation/PSReader/ApplicationSearchDelegate`` take each
  publication’s type from the shortcode’s configuration.
- Manual carousel sections use their
  ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/searchPublicationType``.
- A delegate of your own sets ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchPublication/searchType``.
- In a custom UI, ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedSearchService`` takes the type with each
  publication GUID.

If a publication never returns results, ask PageSuite which type it’s
indexed as.

## Customizing the Search Screen

[`SearchConfiguration`](/documentation/PSReader/SearchConfiguration) styles the prebuilt screen: the header, search
field, and filter pill colors, the label styles for pills, result cells,
and error messages, and the formatter for result dates. It starts from
your [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration)’s fonts and brand color, and takes the
account GUID and time zone that searches use from it too:

```swift
var searchConfig = SearchConfiguration(globalConfig: globalConfig)
searchConfig.selectedPillBackgroundColor = .systemIndigo
searchConfig.resultTitleLabel.pointSize = 18
```

Pass it to the carousel’s `.search(config:)` section or to
[`SearchViewController`](/documentation/PSReader/SearchViewController), or set it as [`search`](/documentation/PSReader/ReaderConfiguration/search) for
search inside the reader. Outside the carousel, a configuration you set on
the reader needs its own search delegate. To force light or dark mode on
the search screen, set [`overrideUserInterfaceStyle`](/documentation/PSReader/SearchViewController/overrideUserInterfaceStyle).
See [Theming](/documentation/PSReader/Theming) for the SDK’s theming as a whole.

## Paywalls and Analytics

The search screen asks your paywall delegate’s
[`paywallViewControllerForAction(openSearchResult:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openSearchResult:))
before it opens a result, not the method that gates opening editions.
It returns `nil` unless you implement it, so if your editions are
paywalled, implement it too; see [Gating Search Results](/documentation/PSReader/Paywalls#Gating-Search-Results).

The screen reports each new query’s first page of results and each
tapped result as analytics events; see [Search](/documentation/PSReader/Analytics#Search).

## Topics

### Search Screen

[`SearchViewController`](/documentation/PSReader/SearchViewController)

A standalone view controller for searching edition content.

### Choosing the Publications

[`SearchDelegate`](/documentation/PSReader/SearchDelegate)

A delegate that provides the list of searchable publications and their reader configurations.

[`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate)

A [`SearchDelegate`](/documentation/PSReader/SearchDelegate) that derives search publications from a `PSAppConfig`
or fetches one lazily from a shortcode.

[`SearchPublication`](/documentation/PSReader/SearchPublication)

A publication that can be searched within using the PageSuite search API.

[`SearchPublicationType`](/documentation/PSReader/SearchPublicationType)

The type of a searchable publication.

[`SearchError`](/documentation/PSReader/SearchError)

Errors related to the search delegate.

### Customizing the Search Screen

[`SearchConfiguration`](/documentation/PSReader/SearchConfiguration)

Configuration for the SDK’s built-in search interface.

