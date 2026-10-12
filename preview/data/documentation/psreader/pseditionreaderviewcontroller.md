<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEditionReaderViewController"
  },
  "title" : "PSEditionReaderViewController"
}
-->

# PSEditionReaderViewController

A view controller that presents an edition from PageSuite’s current
system, classic PDF or responsive, as a horizontally paged reader.

```
@MainActor class PSEditionReaderViewController
```

## Overview

The reader renders a [`PSEEditionSource`](/documentation/PSReader/PSEEditionSource)’s HTML and PDF pages,
manages page-asset loading and retry states, and hosts media overlays,
commenting affordances, and advert pages. It deliberately ships without
chrome — navigation bars, page browsers, and settings UI belong to the
host app. Embed it as a child of your own reader screen rather than
presenting it on its own; see [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader).

```swift
let source = try await published.openEditionSource()
let reader = PSEditionReaderViewController()
addChild(reader)
view.addSubview(reader.view)
reader.didMove(toParent: self)
reader.open(edition: source)
```

Customize behavior through the nested delegate protocols; every delegate
is optional. Track reading position with [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) and the
`currentPage` family, navigate with the `scrollTo` family, and attach a
[`PSEScrollCollapseController`](/documentation/PSReader/PSEScrollCollapseController) to collapse your own chrome as the user
scrolls.

The `source` parameter carried by the `scrollTo` methods and echoed by
[`willScrollTo(pageIndex:pagingMode:source:)`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/willScrollTo(pageIndex:pagingMode:source:)) is an
opaque token: the reader forwards whatever you pass, so you can tag
programmatic navigation (for analytics, say) and recognize it when the
delegate fires. Plain swipes report a `nil` source, and the reader tags
its own internal navigation with [`PageJumpNavigationSource`](/documentation/PSReader/PageJumpNavigationSource),
[`ArticleJumpNavigationSource`](/documentation/PSReader/ArticleJumpNavigationSource), [`SectionJumpNavigationSource`](/documentation/PSReader/SectionJumpNavigationSource), and
[`ReloadDataNavigationSource`](/documentation/PSReader/ReloadDataNavigationSource).

## Topics

### Opening

[`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:))

Loads an edition into the reader, replacing any edition currently
open.

[`reloadPageContent()`](/documentation/PSReader/PSEditionReaderViewController/reloadPageContent())

Re-renders the currently loaded pages in place, keeping position.
Use after a change that affects page rendering (say, a font-size
setting).

[`reloadData()`](/documentation/PSReader/PSEditionReaderViewController/reloadData())

Rebuilds all pages from the edition source, keeping position. Use
when the source’s content changed structurally.

### Navigating

[`scrollTo(index:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(index:source:))

Scrolls to the spread at `index` (a spread index in the active
paging mode). The `source` token is echoed to [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol).

[`scrollToFront(source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollToFront(source:))

Scrolls to the edition’s first spread.

[`scrollTo(page:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(page:source:))

Scrolls to the spread containing `page`. No-op if the page isn’t in
the edition.

[`scrollTo(pageGUID:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(pageGUID:source:))

Scrolls to the spread containing the page with `pageGUID`. No-op if
no page matches.

[`scrollTo(article:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(article:source:))

Scrolls to the spread presenting `article`. No-op if the article
isn’t in the edition.

[`scrollTo(articleGUID:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(articleGUID:source:))

Scrolls to the spread presenting the article with `articleGUID`.
No-op if no article matches.

[`scrollTo(section:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(section:source:))

Scrolls to the first article spread of `section`. No-op if the
section isn’t in the edition.

[`scrollTo(sectionGUID:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(sectionGUID:source:))

Scrolls to the first article spread of the section with
`sectionGUID`. No-op if no section matches.

### Current State

[`currentPage()`](/documentation/PSReader/PSEditionReaderViewController/currentPage())

The current spread’s reference page (in double-page mode, the page
that best represents the spread), or `nil` when no edition is open.

[`currentPageSpread()`](/documentation/PSReader/PSEditionReaderViewController/currentPageSpread())

The spread on screen and the paging mode it was built for, or `nil`
when no edition is open.

[`currentPageIndex()`](/documentation/PSReader/PSEditionReaderViewController/currentPageIndex())

The index of the current reference page within `edition.pages`
(page-level, unlike [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol)’s spread indices), or `nil`
when no edition is open.

[`currentPageViewController()`](/documentation/PSReader/PSEditionReaderViewController/currentPageViewController())

The view controller rendering the current spread, or `nil` before
content settles.

[`PSEditionPageViewController`](/documentation/PSReader/PSEditionPageViewController)

A view controller the reader pages between — one per spread.

[`scrollView()`](/documentation/PSReader/PSEditionReaderViewController/scrollView())

The reader’s horizontal paging scroll view — for gesture
coordination or scroll observation. Don’t mutate its content.

### Delegates

[`scrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/scrollDelegate-swift.property)

Receives paging and zoom events. Optional.

[`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol)

Reports the reader’s paging and zoom activity.

[`mediaDelegate`](/documentation/PSReader/PSEditionReaderViewController/mediaDelegate-swift.property)

Handles media hotspots and embeds. Optional.

[`PSEditionReaderViewController.MediaDelegate`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol)

Handles media hotspots and embeds on the reader’s pages.

[`errorDelegate`](/documentation/PSReader/PSEditionReaderViewController/errorDelegate-swift.property)

Supplies branded failure views. Optional; localized defaults apply.

[`PSEditionReaderViewController.ErrorDelegate`](/documentation/PSReader/PSEditionReaderViewController/ErrorDelegate-swift.protocol)

Supplies the views shown when content fails.

[`commentingDelegate`](/documentation/PSReader/PSEditionReaderViewController/commentingDelegate-swift.property)

Integrates article commenting. Optional; no commenting UI without it.

[`PSEditionReaderViewController.CommentingDelegate`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol)

Integrates an article-commenting system into the reader’s pages.

[`advertDelegate`](/documentation/PSReader/PSEditionReaderViewController/advertDelegate-swift.property)

Overrides advert-page rendering. Optional; built-in rendering applies.

[`PSEditionReaderViewController.AdvertDelegate`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol)

Overrides how advert pages render.

### Handling Link Taps

[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification)

Posted when the user taps a link inside edition content — an article
hyperlink, a link hotspot, or a link out of an advert page.

[`linkTappedURLKey`](/documentation/PSReader/PSEditionReaderViewController/linkTappedURLKey)

The `userInfo` key carrying the tapped `URL` in
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification).

### Laying Out Pages

[`layoutDelegate`](/documentation/PSReader/PSEditionReaderViewController/layoutDelegate-swift.property)

Chooses single- or double-page mode. Optional; single-page without it.

[`PSEditionReaderViewController.LayoutDelegate`](/documentation/PSReader/PSEditionReaderViewController/LayoutDelegate-swift.protocol)

Decides between single-page and double-page presentation.

[`pdfLayoutMode`](/documentation/PSReader/PSEditionReaderViewController/pdfLayoutMode)

How PDF pages fit the viewport: width-filling (scroll vertically to
read) or whole-page. Applies to current and future pages.

### Collapsing Chrome

[`scrollCollapseController`](/documentation/PSReader/PSEditionReaderViewController/scrollCollapseController)

Collapses and reveals host chrome in response to the reader’s
scrolling. Attach one and register your chrome animations on it; the
reader feeds it scroll activity from every page.

