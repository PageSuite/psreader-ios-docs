<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Building-a-Search-Screen",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Building a Search Screen"
}
-->

# Building a Search Screen

Build your own search screen that searches your publications’ editions with the SDK’s search service and opens results in your own reader screen.

## Overview

The prebuilt search screen sends the user’s query when they submit it,
lists the matching articles and pages with a filter for each, and opens a
tapped result’s edition at its page. In a custom UI, you build that
screen yourself. [`FeedSearchService`](/documentation/PSReader/FeedSearchService) is the search API underneath it, without
the screen: give it your account GUID, the query, what to search for, and
the publications to search, and it returns a page of results.

Using the prebuilt UI? See [Search](/documentation/PSReader/Search).

```swift
let service = FeedSearchService()

service.search(
    accountGuid: "ACCOUNT_GUID",
    query: "harbor bridge",
    type: .all,
    publications: [(.app, "PUBLICATION_GUID")]
) { result in
    DispatchQueue.main.async {
        switch result {
        case .success(let response):
            print(response.meta?.totalCount ?? 0, "matches")
            for match in response.data ?? [] {
                print(match.headline ?? "Page \(match.pageNumber ?? 0)")
            }
        case .failure(let error):
            print(error)
        }
    }
}
```

The completion handler runs on a background queue, so move to the main
queue before you update your interface.

The sections below build `SearchScreenViewController`, a table view
controller with a search bar in its navigation item. It searches when the
user submits a query, loads more results as they scroll, and opens a
result in `ReaderScreenViewController`, the reader screen from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader). `showAlert(title:error:)` is the sample app’s
alert helper, an extension on `UIViewController`.

## Sending a Query

Each publication goes into the request as a pair: its search type and its
publication GUID. The type must match how PageSuite indexes the
publication, [`SearchPublicationType.app`](/documentation/PSReader/SearchPublicationType/app) or
[`SearchPublicationType.publication`](/documentation/PSReader/SearchPublicationType/publication), or that publication returns no
results; see [Matching the Search Type](/documentation/PSReader/Search#Matching-the-Search-Type). The `type` parameter
filters what comes back: [`SearchType.all`](/documentation/PSReader/SearchType/all) results, or only
[`SearchType.editionArticle`](/documentation/PSReader/SearchType/editionArticle) or [`SearchType.editionPage`](/documentation/PSReader/SearchType/editionPage) results, like
the prebuilt screen’s filter pills.

Send queries of at least three characters, not counting spaces at either
end. The search backend needs that many, and the prebuilt screen waits
for them. It searches when the user submits the query rather than on
every keystroke, and so does this screen:

```swift
final class SearchScreenViewController: UITableViewController, UISearchBarDelegate {

    let service = FeedSearchService()
    let publications: [(type: SearchPublicationType, id: String)] = [
        (.app, "PUBLICATION_GUID")
    ]

    var query = ""
    var filter = SearchType.all
    var results: [SearchResult] = []
    var totalCount = 0

    private var task: URLSessionDataTask?
    private var searchGeneration = 0

    override func viewDidLoad() {
        super.viewDidLoad()
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "Result")

        let searchController = UISearchController(searchResultsController: nil)
        searchController.searchBar.delegate = self
        navigationItem.searchController = searchController
    }

    func searchBarSearchButtonClicked(_ searchBar: UISearchBar) {
        searchBar.resignFirstResponder()

        let query = (searchBar.text ?? "").trimmingCharacters(in: .whitespacesAndNewlines)
        guard query.count >= 3 else { return }

        self.query = query
        runSearch(appending: false)
    }

    func runSearch(appending: Bool) {
        task?.cancel()
        searchGeneration += 1
        let generation = searchGeneration

        task = service.search(
            accountGuid: "ACCOUNT_GUID",
            query: query,
            type: filter,
            publications: publications,
            offset: appending ? results.count : 0
        ) { [weak self] result in
            DispatchQueue.main.async {
                // Drop the answer to a search that a newer one replaced.
                guard let self, self.searchGeneration == generation else { return }
                self.task = nil
                self.show(result, appending: appending)
            }
        }
    }
}
```

The search method returns the request’s `URLSessionDataTask`. Cancel it
when a new search starts, so that a slow answer to an old query can’t
replace the new one’s results. A canceled request still calls its
completion handler, with a cancellation error, and the generation check
drops that answer along with any other stale one.

## Showing Results

Each [`SearchResponse`](/documentation/PSReader/SearchResponse) holds one page of [`SearchResult`](/documentation/PSReader/SearchResult) values in
[`data`](/documentation/PSReader/SearchResponse/data), and the total number of matches in
[`meta`](/documentation/PSReader/SearchResponse/meta-swift.property):

```swift
func show(_ result: Result<SearchResponse, Error>, appending: Bool) {
    switch result {
    case .success(let response):
        let page = response.data ?? []
        results = appending ? results + page : page
        totalCount = response.meta?.totalCount ?? 0
        tableView.reloadData()
    case .failure(let error):
        showAlert(title: "Couldn't Search", error: error)
    }
}
```

These properties describe a result:

|Property                                                                                                                                                                                                                                |Holds                                                                                                                                                                                                   |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/type``                                                                                                                                                               |``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/editionArticleType`` for an article, ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/editionPageType`` for a page.|
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/editionId``                                                                                                                                                          |The edition GUID.                                                                                                                                                                                       |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/pageId``                                                                                                                                                             |The GUID of the page to open.                                                                                                                                                                           |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/applicationId``                                                                                                                                                      |The publication GUID.                                                                                                                                                                                   |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/publicationId``                                                                                                                                                      |Another publication identifier the search API can return.                                                                                                                                               |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/headline``, ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/section``, ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/author``|The article’s headline, section name, and author, for article results.                                                                                                                                  |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/pageNumber``                                                                                                                                                         |The page number, for page results.                                                                                                                                                                      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/snippet``                                                                                                                                                            |The matching text, with `<b>` tags around the matched terms.                                                                                                                                            |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/images``                                                                                                                                                             |Images for the result, with URLs and captions.                                                                                                                                                          |
|``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/parsedEditionDate``                                                                                                                                                  |The edition date. ``doc://com.pagesuite.PSReader/documentation/PSReader/SearchResult/editionDate`` is the raw string.                                                                                   |

[`formattedSnippet(font:)`](/documentation/PSReader/SearchResult/formattedSnippet(font:)) turns the snippet’s `<b>` tags
into bold text. A cell that shows an article’s headline, or a page’s
number, above the snippet:

```swift
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    results.count
}

override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let result = results[indexPath.row]
    let cell = tableView.dequeueReusableCell(withIdentifier: "Result", for: indexPath)

    var content = cell.defaultContentConfiguration()
    if result.type == SearchResult.editionArticleType {
        content.text = result.headline
    } else {
        content.text = "Page \(result.pageNumber ?? 0)"
    }
    content.secondaryAttributedText = result.formattedSnippet(
        font: .preferredFont(forTextStyle: .subheadline)
    )
    cell.contentConfiguration = content
    return cell
}
```

To show which publication a result comes from, match its `applicationId`
against your publication list, falling back to `publicationId`, as the
prebuilt screen does. [`publicationName`](/documentation/PSReader/SearchResult/publicationName) is filled in only
by the prebuilt screen; results from [`FeedSearchService`](/documentation/PSReader/FeedSearchService) leave it `nil`.

## Loading More Results

Results come a page at a time. The `offset` and `limit` parameters choose
the page, and by default a search returns the first 50 results. To load
more, request the next page at an `offset` equal to the number of results
you have, until you reach [`totalCount`](/documentation/PSReader/SearchResponse/Meta-swift.struct/totalCount).
The prebuilt screen does it as the user nears the end of the list:

```swift
override func tableView(_ tableView: UITableView,
                        willDisplay cell: UITableViewCell,
                        forRowAt indexPath: IndexPath) {
    let isLastRow = indexPath.row == results.count - 1
    if isLastRow, results.count < totalCount, task == nil {
        runSearch(appending: true)
    }
}
```

`runSearch(appending:)` from [Sending a Query](/documentation/PSReader/Building-a-Search-Screen#Sending-a-Query)
sends the current result count as the offset and appends the page that
comes back. If loading more fails, keep the results you have and offer a
retry at the end of the list, as the prebuilt screen does.

## Filtering by Publication and Date

To search one publication, as the prebuilt screen’s publication menu
does, pass only that publication. To change what comes back, set
`filter` and search again.

To limit a search to a date range, use
[`search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)`](/documentation/PSReader/FeedSearchService/search(accountGuid:query:type:publications:fromDate:toDate:offset:limit:timeZone:completion:)).
It applies the range only when you pass both dates, and sends them as
calendar days in `timeZone`, the device’s time zone by default:

```swift
let lastWeek = Date.now.addingTimeInterval(-7 * 24 * 60 * 60)

task = service.search(
    accountGuid: "ACCOUNT_GUID",
    query: query,
    type: filter,
    publications: publications,
    fromDate: lastWeek,
    toDate: .now
) { [weak self] result in
    // Handle the result as runSearch(appending:) does.
}
```

## Opening a Result

A result carries its edition GUID and page GUID, not the edition.
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)) resolves the edition,
including editions older than the archive returns. Hand it to your reader
screen with the result’s page GUID, and the screen opens the edition on
that page:

```swift
override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    let result = results[indexPath.row]

    Task {
        do {
            try await open(result)
        } catch {
            showAlert(title: "Couldn't Open Edition", error: error)
        }
    }
}

func open(_ result: SearchResult) async throws {
    guard let editionGUID = result.editionId else { return }

    let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
    let published = try await service.published(forEditionGUID: editionGUID)

    let reader = UINavigationController(
        rootViewController: ReaderScreenViewController(published: published, openingPageGUID: result.pageId)
    )
    reader.modalPresentationStyle = .fullScreen
    present(reader, animated: true)
}
```

For more on opening by edition GUID, see
[Opening From an Edition GUID](/documentation/PSReader/Opening-an-Edition#Opening-From-an-Edition-GUID).

An edition resolved this way has an empty
[`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID) and [`publicationName`](/documentation/PSReader/PSEPublished/publicationName).
When you need the publication GUID, to decide on a paywall or to report
analytics, read the result’s `applicationId` (see [Identifiers](/documentation/PSReader/Identifiers)).
Without a publication name, your reader screen’s title is the edition’s
name; to show the publication’s, look its name up from the result’s
`applicationId` in your own list of publications and set
`publicationName` on the entry before you create the screen. If your editions are behind a
paywall, check access at the top of `open(_:)`; see
[Gating Search Results](/documentation/PSReader/Gating-Editions-Behind-a-Paywall#Gating-Search-Results). If you
report analytics from your reader screen, give it the result’s
publication GUID too; see [Reporting From Your Reader Screen](/documentation/PSReader/Reporting-Analytics#Reporting-From-Your-Reader-Screen).

## Opening Results in the Prebuilt Reader

To list results in your own screen but read them in the prebuilt reader,
pass each result’s identifiers to [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController):

```swift
guard let editionGUID = result.editionId,
      let publicationGUID = result.applicationId ?? result.publicationId else { return }

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    publicationGUID: publicationGUID,
    editionGUID: editionGUID,
    openingPage: result.pageId.map { .page(guid: $0) }
)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

The prebuilt reader asks your paywall delegate’s
[`paywallViewControllerForAction(openFeedEdition:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openFeedEdition:)) as it
does for any edition, so no separate check is needed; see [Paywalls](/documentation/PSReader/Paywalls).

## Reporting Searches

The prebuilt search screen reports a completed search and a tapped
result as analytics events. [`FeedSearchService`](/documentation/PSReader/FeedSearchService) reports nothing, so
report them yourself: a search when the first page of results for a new
query arrives, even an empty one, and a tap before you open the result.

```swift
// In show(_:appending:), when appending is false:
ReaderAnalytics.track("searchCompleted", properties: [
    "query": query,
    "results": totalCount,
])

// At the top of open(_:):
ReaderAnalytics.track("searchResultTapped", properties: [
    "query": query,
    "headline": result.headline ?? "",
])
```

`ReaderAnalytics` is your reporting function; see [Reporting Analytics](/documentation/PSReader/Reporting-Analytics),
which also explains why these are the prebuilt UI’s event names.

## Topics

### Sending a Query

[`FeedSearchService`](/documentation/PSReader/FeedSearchService)

A [`SearchService`](/documentation/PSReader/SearchService) for searching editions on PageSuite’s current system.

[`SearchService`](/documentation/PSReader/SearchService)

A service for searching PageSuite edition content.

[`SearchType`](/documentation/PSReader/SearchType)

The type of content to search for.

### Showing Results

[`SearchResponse`](/documentation/PSReader/SearchResponse)

The response from a search request.

[`SearchResult`](/documentation/PSReader/SearchResult)

A single search result returned by the PageSuite search API.

