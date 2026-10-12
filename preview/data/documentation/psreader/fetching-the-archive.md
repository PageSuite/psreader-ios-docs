<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Fetching-the-Archive",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Fetching the Archive"
}
-->

# Fetching the Archive

Load a publication’s editions and draw your own archive screen.

## Overview

[`FeedEditionService`](/documentation/PSReader/FeedEditionService) lists the editions a publication has published,
newest first. Each entry is a [`PSEPublished`](/documentation/PSReader/PSEPublished): it carries the cover image,
name, and date an archive cell shows, and it opens straight into the
reader. The catalog works the same for every publication on PageSuite’s
current edition system, whether its editions are classic PDF pages,
responsive pages, or a mix of both.

```swift
import PSReader

let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
let archive = try await service.publishedEditions(
    publicationGUID: "PUBLICATION_GUID",
    publicationName: "The Daily"
)

for day in archive {
    for published in day.editions ?? [] {
        print(published.name, published.image)
    }
}
```

Using the prebuilt UI? Its archive comes ready-made; see
[Setting Up the Carousel](/documentation/PSReader/Setting-Up-the-Carousel). For where the account and publication GUIDs
come from, see [Identifiers](/documentation/PSReader/Identifiers).

## Initialize the SDK

Call [`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:)) once at launch, as
[Getting Started](/documentation/PSReader/Getting-Started) shows. You don’t need to wait for it before you load the catalog.

## Load the Catalog

Create one [`FeedEditionService`](/documentation/PSReader/FeedEditionService) for your account and ask it for a
publication’s catalog by **publication GUID**, with the publication’s
name:

```swift
let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
let archive = try await service.publishedEditions(
    publicationGUID: "PUBLICATION_GUID",
    publicationName: "The Daily"
)
```

The result is an array of [`PSEPublishedDate`](/documentation/PSReader/PSEPublishedDate) groups, newest first: each
group’s `editions` are the editions published on its `date`, ready to
render as a dated grid. Editions published on the same day come in the
backend’s order; sort them yourself, by `datePublished` for example, if
your grid needs a particular order.

The catalog doesn’t carry the publication’s name, so the service copies
the name you pass onto each edition’s [`publicationName`](/documentation/PSReader/PSEPublished/publicationName).
Your reader screen shows it as its title (see
[Presenting the Screen](/documentation/PSReader/Hosting-the-Reader#Presenting-the-Screen)); without it, the property
is empty.

For a “read the latest issue” entry point, skip the grouping:

```swift
let latest = try await service.latestEdition(
    publicationGUID: "PUBLICATION_GUID",
    publicationName: "The Daily"
)
```

An archive you’ve already fetched gives the same answer through
`archive.latestEdition`.

## Draw the Covers

Each [`PSEPublished`](/documentation/PSReader/PSEPublished) carries what an archive cell shows:

```swift
cell.title = published.name
cell.date = published.editionDate ?? published.datePublished
cell.coverURL = URL(string: published.image)   // the cover thumbnail
```

To show the date the way the prebuilt archive does, format it with
[`DefaultEditionDateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter). Some editions are named rather than
dated, such as a special issue. When
[`useCustomEditionName`](/documentation/PSReader/PSEPublished/useCustomEditionName) is `true`, show the `name` where
you’d otherwise show the date.

Tapping a cell opens the edition in your reader screen:
`ReaderScreenViewController(published:)`, from [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader),
opens it with progress. [Opening an Edition](/documentation/PSReader/Opening-an-Edition) covers the other ways to
open one. To badge editions that are saved for offline reading, check
[`isDownloaded(published:)`](/documentation/PSReader/PSEDownloadManager/isDownloaded(published:)); see
[Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button).

## Handle Errors and Offline Use

The catalog keeps working offline. When the request fails, the service
answers with its cached copy of the last catalog it fetched for that
publication, when it still has one. With nothing cached to fall back on, it
throws
[`FeedEditionServiceError.invalidResponse`](/documentation/PSReader/FeedEditionServiceError/invalidResponse).

[`latestEdition(publicationGUID:publicationName:publishedDomain:)`](/documentation/PSReader/FeedEditionService/latestEdition(publicationGUID:publicationName:publishedDomain:))
throws [`FeedEditionServiceError.editionNotFound`](/documentation/PSReader/FeedEditionServiceError/editionNotFound) when the publication has
nothing published yet. The date-range listing
([Browse by Date](/documentation/PSReader/Fetching-the-Archive#Browse-by-Date)) has no offline fallback: it passes transport
errors, such as `URLError` when the device is offline, through unchanged.

## Browse by Date

A month picker over a long archive shouldn’t load the whole catalog. Ask
for a range of calendar days instead:

```swift
let page = try await service.publishedEditions(
    publicationGUID: "PUBLICATION_GUID",
    publicationName: "The Daily",
    startDate: "2026-09-01",
    endDate: "2026-09-30",
    pageSize: 100
)
let days = page.dates ?? []
```

Both days are inclusive, written `yyyy-MM-dd`, and read in the
publication’s time zone. Results are paged by publishing date, not by
edition: `pageSize` counts [`PSEPublishedDate`](/documentation/PSReader/PSEPublishedDate) groups, from 1 to 100
(25 by default), so a calendar month always fits in one page of 100. For
longer ranges, keep requesting the next `pageNumber` while
`page.pagination?.hasNext == true`.

A range without editions returns an empty page, and so does a day the
backend can’t read or an `endDate` before `startDate`. Every field of the
page is optional, so one malformed field never discards the rest. As with
the full catalog, pass `publicationName` and the service sets it on each
[`PSEPublished`](/documentation/PSReader/PSEPublished).

> Important: The date-range listing serves publications on PageSuite’s v1
> publications API. For any other publication it throws
> ``doc://com.pagesuite.PSReader/documentation/PSReader/FeedEditionServiceError/publicationNotFound``, even though the full
> catalog loads. Catch that error and fall back to the full catalog,
> filtering its editions by `datePublished`.

### Listing One Month

For a month picker, ask for the month’s first and last days, written as
`yyyy-MM-dd`. Publications the date-range listing doesn’t serve throw
[`FeedEditionServiceError.publicationNotFound`](/documentation/PSReader/FeedEditionServiceError/publicationNotFound); for those, filter the
full archive instead:

```swift
func editions(inMonthOf month: Date) async throws -> [PSEPublished] {
    var calendar = Calendar(identifier: .gregorian)
    calendar.timeZone = .current

    let formatter = DateFormatter()
    formatter.calendar = calendar
    formatter.locale = Locale(identifier: "en_US_POSIX")
    formatter.dateFormat = "yyyy-MM-dd"

    guard let interval = calendar.dateInterval(of: .month, for: month),
          let lastDay = calendar.date(byAdding: .day, value: -1, to: interval.end) else {
        return []
    }

    do {
        let page = try await service.publishedEditions(
            publicationGUID: "PUBLICATION_GUID",
            publicationName: "The Daily",
            startDate: formatter.string(from: interval.start),
            endDate: formatter.string(from: lastDay),
            pageSize: 100
        )
        return (page.dates ?? []).flatMap { $0.editions ?? [] }
    } catch FeedEditionServiceError.publicationNotFound {
        let archive = try await service.publishedEditions(
            publicationGUID: "PUBLICATION_GUID",
            publicationName: "The Daily"
        )
        return archive.flatMap { $0.editions ?? [] }.filter { published in
            guard let date = published.editionDate ?? published.datePublished else { return false }
            return calendar.isDate(date, equalTo: month, toGranularity: .month)
        }
    }
}
```

## Combine Several Publications

An account can host several publications. There’s no separate
multi-publication call; compose one from the service. Fetch per publication
GUID, then lay the results out however your product needs: a kiosk grid of
latest covers, a combined list, or a tab per title.

```swift
let publications = [
    (guid: "PUBLICATION_GUID", name: "The Daily"),
    (guid: "WEEKEND_PUBLICATION_GUID", name: "The Weekend")
]

let latestCovers = try await withThrowingTaskGroup(of: (String, PSEPublished).self) { group in
    for publication in publications {
        group.addTask {
            let latest = try await service.latestEdition(
                publicationGUID: publication.guid,
                publicationName: publication.name
            )
            return (publication.guid, latest)
        }
    }
    return try await group.reduce(into: [String: PSEPublished]()) { $0[$1.0] = $1.1 }
}
```

## Resolve an Edition GUID

Search results and deep links often carry only an edition GUID. Resolve it
with [`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)), which also finds
editions older than the catalog returns. The entry it returns has no
publication name or publication GUID; see
[Opening From an Edition GUID](/documentation/PSReader/Opening-an-Edition#Opening-From-an-Edition-GUID).

## Load the Content Model

You don’t need the service to read an edition: the reader opens a
[`PSEPublished`](/documentation/PSReader/PSEPublished) directly (see [Opening an Edition](/documentation/PSReader/Opening-an-Edition)).
[`edition(for:)`](/documentation/PSReader/FeedEditionService/edition(for:)) loads an edition’s full content model,
[`PSEEdition`](/documentation/PSReader/PSEEdition), for the rarer case of consuming its pages and articles
yourself, such as building your own index or search over them.

## Topics

### Fetching the Catalog

[`FeedEditionService`](/documentation/PSReader/FeedEditionService)

Fetches catalogs and content of editions on PageSuite’s current system
for an account.

