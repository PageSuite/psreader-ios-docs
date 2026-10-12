<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/The-Edition-Model",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "The Edition Model"
}
-->

# The Edition Model

How publications, editions, spreads, pages, and articles fit together.

## Overview

Every edition on PageSuite’s current system, classic PDF or responsive,
arrives as the same family of model types. They come in two layers: a
light **catalog** layer for listing editions, and a **content** layer you
get when you open one.

```
PSEPublishedDate          one archive date
└─ PSEPublished           one edition in the catalog
   └─ PSEEdition          its loaded content
      ├─ PSEPageSpread    one reader screenful
      │  └─ PSEPage       one page
      │     └─ PSEArticle one article on the page
      └─ PSESection       a named group of articles
```

|Type                                                                    |Role                                                    |
|------------------------------------------------------------------------|--------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublishedDate``|One archive date and the editions published on it.      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished``    |A catalog entry: identity, cover image, dates.          |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEdition``      |The loaded content: pages, spreads, sections.           |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPageSpread``   |One reader screenful: one page, or two facing pages.    |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage``         |A PDF page, a templated article page, or an advert page.|
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEArticle``      |Editorial content presented on a page.                  |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSESection``      |A named grouping of the edition’s articles.             |

You work with these types directly in a custom UI. The prebuilt UI hands
you the same types in its delegate callbacks and analytics events, so
they’re worth knowing on either side.

## The Catalog Layer

[`FeedEditionService`](/documentation/PSReader/FeedEditionService) returns a publication’s archive as an array of
[`PSEPublishedDate`](/documentation/PSReader/PSEPublishedDate), newest first, each holding the
[`PSEPublished`](/documentation/PSReader/PSEPublished) editions released that day. A published edition is
small: enough to draw an archive cell and to open the edition.

```swift
let archive = try await service.publishedEditions(publicationGUID: "PUBLICATION_GUID")
let editions = archive.flatMap { $0.editions ?? [] }   // newest first

for published in editions {
    print(published.name, published.image)   // display name, cover URL
}
```

[`publishedGUID`](/documentation/PSReader/PSEPublished/publishedGUID) identifies the catalog entry. Downloads and
bookmarks are keyed by it, and so should anything you store per edition.
See [Identifiers](/documentation/PSReader/Identifiers) for the rest.

## The Content Layer

Opening a published edition gives you a [`PSEEditionSource`](/documentation/PSReader/PSEEditionSource), whose
[`edition`](/documentation/PSReader/PSEEditionSource/edition) is the [`PSEEdition`](/documentation/PSReader/PSEEdition): every page in reading
order, the spreads the reader pages between, and the sections.

```swift
let source = try await published.openEditionSource()
let edition = source.edition

let pageCount = edition.pages?.count ?? 0
let sections = edition.sections ?? []
```

See [Opening an Edition](/documentation/PSReader/Opening-an-Edition) for the ways to open one.

## Pages and Spreads

[`pages`](/documentation/PSReader/PSEEdition/pages) holds every page in reading order. The reader,
however, pages between **spreads**. In single-page mode each spread is one
page; in double-page mode it’s two facing pages, or one when a page stands
alone, such as the cover. [`pageSpreads(for:)`](/documentation/PSReader/PSEEdition/pageSpreads(for:)) returns the
spreads for a [`PSEditionPagingMode`](/documentation/PSReader/PSEditionPagingMode).

Reader callbacks report spread indices, not page indices. Translate
between the two with the edition’s helpers:

```swift
// From a reader callback's spread index to the page it shows.
let page = edition.pageSpread(atIndex: index, pagingMode: pagingMode)?.referencePage()

// From a page back to its spread index, to highlight it in a page browser.
let spreadIndex = edition.pageIndex(for: selectedPage, inPagingMode: pagingMode)
```

[`referencePage()`](/documentation/PSReader/PSEPageSpread/referencePage()) prefers editorial content, so a spread
pairing an advert with an article page reports the article page.

## Pages

A page’s [`type`](/documentation/PSReader/PSEPage/type) says what it is: a PDF page, a templated
article or section page, or an advert. The common questions have their
own properties: [`isPDF`](/documentation/PSReader/PSEPage/isPDF), [`isAdvertPage`](/documentation/PSReader/PSEPage/isAdvertPage), and
[`hasResizableText`](/documentation/PSReader/PSEPage/hasResizableText).

Pages carry what’s on them: [`articles`](/documentation/PSReader/PSEPage/articles), the interactive
hotspots in [`mediaObjects`](/documentation/PSReader/PSEPage/mediaObjects), [`adverts`](/documentation/PSReader/PSEPage/adverts), and
[`puzzles`](/documentation/PSReader/PSEPage/puzzles). [`effectiveScreenshotURL`](/documentation/PSReader/PSEPage/effectiveScreenshotURL) is the page’s
thumbnail.

## Friendly Page Labels

Publishers often label pages the way they’re printed, such as “A1” or
“B12”, rather than by number. Show [`pageLabel`](/documentation/PSReader/PSEPage/pageLabel) wherever you
name a page: it’s the publisher’s label when the edition has one, and the
page number otherwise, so it’s always safe to show.

```swift
pageTitle.text = "Page \(page.pageLabel)"   // "Page A1", or "Page 3"
```

In double-page mode a spread shows two pages. Label it from its pages,
leaving out advert pages, which aren’t printed pages:

```swift
func title(for spread: PSEPageSpread) -> String? {
    let labels = spread.nonAdvertPages().map(\.pageLabel)
    guard !labels.isEmpty else { return nil }   // an advert-only spread

    return "Page " + labels.joined(separator: "–")   // "Page A2–A3"
}
```

What goes into a label:

- **The publisher’s label.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/friendlyPageName`` is the label
  alone, or `nil` when there’s none. Whole editions, or single pages, may
  lack one; check this property when you need to know whether the
  publisher supplied a label.
- **Article pages borrow theirs.** A templated article page has no label
  of its own, so it shows the label of the PDF page that links to it.
- **The page number.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/pageNumber`` is the printed page number,
  which `pageLabel` falls back to. Advert pages aren’t printed pages and
  usually report `0`, so check ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/isAdvertPage`` before labeling a
  page, and don’t build labels from `pageNumber` yourself.

Labels are free text from the publisher, such as “A1”, “Sport 4”, or
“iv”. Don’t parse them: to sort or compare pages, use their order in
[`pages`](/documentation/PSReader/PSEEdition/pages). Localize the word “Page” that goes with them; the
prebuilt UI uses [`LocalizedStringKey.page`](/documentation/PSReader/LocalizedStringKey/page), which you can override (see
[Localization](/documentation/PSReader/Localization)).

The prebuilt UI shows friendly labels in its content browser, its
bookmarks, and its share messages; its search results show page numbers.
In a custom UI, show them in your own chrome and page browser; see
[Labeling Spreads](/documentation/PSReader/Hosting-the-Reader#Labeling-Spreads) and [Building a Page Browser](/documentation/PSReader/Building-a-Page-Browser).

## Articles and Sections

A [`PSEArticle`](/documentation/PSReader/PSEArticle) holds an article’s text and media: [`headline`](/documentation/PSReader/PSEArticle/headline),
[`story`](/documentation/PSReader/PSEArticle/story) (the body, as HTML), [`images`](/documentation/PSReader/PSEArticle/images), and
[`videos`](/documentation/PSReader/PSEArticle/videos), among others. Articles appear on the pages that
present them, and again under the [`PSESection`](/documentation/PSReader/PSESection) they belong to.

Sections group articles by subject, such as News or Sport.
[`pageBrowserSections`](/documentation/PSReader/PSEEdition/pageBrowserSections) groups pages the same way for a page
browser. See [Building a Page Browser](/documentation/PSReader/Building-a-Page-Browser).

> Note: Model property names mirror the backend payload and are part of
> the shipped API, casing included: ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/pageguid``,
> ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEArticle/articleguid``, ``doc://com.pagesuite.PSReader/documentation/PSReader/PSESection/sectionguid``.

## Topics

### The Catalog Layer

[`PSEPublished`](/documentation/PSReader/PSEPublished)

A published edition in a publication’s catalog — the unit an archive
lists and everything else opens.

### The Content Layer

[`PSEEdition`](/documentation/PSReader/PSEEdition)

The loaded content of an edition: its pages, precomputed spreads, and
sections.

[`PSEPageSpread`](/documentation/PSReader/PSEPageSpread)

One reader screenful: a single page, or two facing pages in double-page
mode.

[`PSEPage`](/documentation/PSReader/PSEPage)

A single page of an edition — a rendered PDF page, a templated HTML
article page, or a dedicated advert page.

[`PSEArticle`](/documentation/PSReader/PSEArticle)

An editorial article, with its text, imagery, and metadata.

