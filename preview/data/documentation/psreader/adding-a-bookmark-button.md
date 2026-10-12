<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Adding-a-Bookmark-Button",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Adding a Bookmark Button"
}
-->

# Adding a Bookmark Button

Add a bookmark button to your own reader screen that saves the page or article in view, then list and reopen what the user saved.

## Overview

The prebuilt reader has a bookmark button in its navigation bar, and a
Bookmarks screen that lists saved items and reopens them, offline too.
In your own reader screen you build the button and the list, and
[`shared`](/documentation/PSReader/PSEBookmarkManager/shared) keeps the bookmarks: each one saves an
article or a whole page, with its own copy of the content, so it reopens
without a network connection.

Using the prebuilt UI? See [Bookmarks](/documentation/PSReader/Bookmarks).

The code on this page is the sample app’s. It adds the button to
`ReaderScreenViewController`, the reader screen from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader). Start with the button, as a property of the
class:

```swift
private lazy var bookmarkButton = UIBarButtonItem(
    image: UIImage(systemName: "bookmark"),
    style: .plain,
    target: self,
    action: #selector(toggleBookmark)
)
```

The prebuilt screens use the same manager. If your app mixes any of them
in, they show the bookmarks your button saves, and your screens show
theirs.

## Showing the Button

In `addChrome()`, put the button in the navigation bar, disabled until
the first page settles:

```swift
bookmarkButton.isEnabled = false
navigationItem.rightBarButtonItems = (navigationItem.rightBarButtonItems ?? []) + [bookmarkButton]
```

In `updateChrome()`, which runs each time the reader settles on a page,
add:

```swift
// Some pages, such as section fronts and adverts, have nothing
// to bookmark.
let context = page.bookmarkContext()
let isBookmarked = PSEBookmarkManager.shared.isBookmarked(context: context)
bookmarkButton.isEnabled = context.isBookmarkable
bookmarkButton.image = UIImage(systemName: isBookmarked ? "bookmark.fill" : "bookmark")
```

The button disables on a page with nothing to bookmark rather than
disappearing, so the bar doesn’t rearrange itself as the user pages.
The other buttons in the custom feature guides follow the same rule.

## Saving and Removing a Bookmark

Add the action in an extension, in the same file as the class:

```swift
extension ReaderScreenViewController {

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
}
```

Toggling throws only when the manager can’t copy the content for
offline reading. Bookmarks need no analytics code of your own:
[`EventChannel`](/documentation/PSReader/EventChannel) observes the manager and reports each bookmark saved or
removed, whichever screen made the change. See [Reporting Analytics](/documentation/PSReader/Reporting-Analytics).

## Keeping the Button in Sync

Bookmarks also change outside your button: from another screen, or from
your own code. To keep the button current, refresh it on
[`bookmarksDidChange`](/documentation/PSReader/PSEBookmarkManager/bookmarksDidChange). In `addChrome()`, add:

```swift
NotificationCenter.default.addObserver(
    self,
    selector: #selector(bookmarksDidChange),
    name: PSEBookmarkManager.bookmarksDidChange,
    object: nil
)
```

And in the extension:

```swift
@objc private func bookmarksDidChange() {
    updateChrome()
}
```

## What Each Page Bookmarks

What a page offers to bookmark depends on its kind, as
[`bookmarkContext()`](/documentation/PSReader/PSEPage/bookmarkContext()) reports:

- A template page that holds one article bookmarks that article.
- PDF and web pages bookmark as whole pages.
- Other pages, such as section fronts, pages with several articles, and
  adverts, have nothing to bookmark; the context’s
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/BookmarkContext/isBookmarkable`` is `false`.

[`PSEBookmark`](/documentation/PSReader/PSEBookmark) covers both kinds of saved item:
[`PSEBookmark.article(_:)`](/documentation/PSReader/PSEBookmark/article(_:)) and [`PSEBookmark.page(_:)`](/documentation/PSReader/PSEBookmark/page(_:)). The
context-based methods choose the right kind for you. To bookmark an
article or page your UI shows outside the reader, the per-kind methods,
such as
[`toggleBookmark(forArticle:in:edition:published:application:)`](/documentation/PSReader/PSEBookmarkManager/toggleBookmark(forArticle:in:edition:published:application:))
and [`isBookmarked(page:)`](/documentation/PSReader/PSEBookmarkManager/isBookmarked(page:)), skip the context.

## Bookmarking Both Pages of a Spread

When the reader shows a double-page spread, the prebuilt reader’s
button covers both pages: one tap saves both, or removes both when both
are saved. To do the same, base the button on the spread on screen.
[`isBookmarked(spread:)`](/documentation/PSReader/PSEBookmarkManager/isBookmarked(spread:)) returns `nil` when the
spread has nothing to bookmark, and otherwise whether all of its
bookmarkable pages are saved.

In `updateChrome()`, replace the bookmark block from
[Showing the Button](/documentation/PSReader/Adding-a-Bookmark-Button#Showing-the-Button) with:

```swift
if let (spread, _) = reader.currentPageSpread(),
   let isBookmarked = PSEBookmarkManager.shared.isBookmarked(spread: spread) {
    bookmarkButton.isEnabled = true
    bookmarkButton.image = UIImage(systemName: isBookmarked ? "bookmark.fill" : "bookmark")
} else {
    bookmarkButton.isEnabled = false   // Nothing on screen to bookmark.
}
```

And replace the action, so a tap saves each page that isn’t saved yet, or
removes them all:

```swift
@objc private func toggleBookmark() {
    guard let source,
          let (spread, _) = reader.currentPageSpread(),
          let isBookmarked = PSEBookmarkManager.shared.isBookmarked(spread: spread) else {
        return
    }

    for page in spread.bookmarkablePages() {
        let context = page.bookmarkContext()

        // Only toggle the pages that aren't in the state the tap asks for.
        guard PSEBookmarkManager.shared.isBookmarked(context: context) == isBookmarked else {
            continue
        }

        do {
            try PSEBookmarkManager.shared.toggleBookmark(
                context: context,
                edition: source.edition,
                published: source.published
            )
        } catch {
            showAlert(title: "Couldn't Bookmark Page", error: error)
        }
    }

    updateChrome()
}
```

If your screen also labels spreads, as in [Labeling Spreads](/documentation/PSReader/Hosting-the-Reader#Labeling-Spreads),
both blocks read the spread. Following both pages as written compiles
cleanly; to read the spread once, bind `reader.currentPageSpread()` at
the top of `updateChrome()` and use it in both blocks.

## Listing Saved Bookmarks

[`bookmarks`](/documentation/PSReader/PSEBookmarkManager/bookmarks) returns every saved bookmark: the article
bookmarks first, then the page bookmarks, each newest first.
[`articleBookmarks`](/documentation/PSReader/PSEBookmarkManager/articleBookmarks) and
[`pageBookmarks`](/documentation/PSReader/PSEBookmarkManager/pageBookmarks) return the two kinds separately, and
[`hasBookmarks`](/documentation/PSReader/PSEBookmarkManager/hasBookmarks) says whether there are any. For one
list ordered by when the items were saved, sort by each bookmark’s
`dateAdded`:

```swift
extension PSEBookmark {
    var dateAdded: Date? {
        switch self {
        case .article(let bookmark): return bookmark.dateAdded
        case .page(let bookmark): return bookmark.dateAdded
        @unknown default: return nil
        }
    }
}

let newestFirst = PSEBookmarkManager.shared.bookmarks.sorted {
    ($0.dateAdded ?? .distantPast) > ($1.dateAdded ?? .distantPast)
}
```

Each record keeps what a list row needs, copied when the item was saved:

- **Article bookmarks** (``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkArticle``): the
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkArticle/article``, with its headline and images; the
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkArticle/section`` it came from; and the edition’s
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkArticle/editionName`` and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkArticle/editionDate``. For a thumbnail,
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkArticle/localThumbnailURL()`` finds a saved copy of the
  article’s image, and ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkArticle/remoteThumbnailURL()`` is the
  fallback.
- **Page bookmarks** (``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkPage``): the ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkPage/page``,
  whose ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/pageLabel`` names it, and the edition’s
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkPage/editionName`` and ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkPage/editionDate``.
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkPage/localThumbnailURL()`` is the saved page image.
- **Either kind:** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmark/published`` is the catalog entry of the
  edition the item came from, when known.

To keep the list current, observe the manager; see
[Observing Changes](/documentation/PSReader/Adding-a-Bookmark-Button#Observing-Changes).

## Opening a Bookmark

[`editionSource(mode:among:onProgress:)`](/documentation/PSReader/PSEBookmark/editionSource(mode:among:onProgress:)) makes the same
choice as the prebuilt Bookmarks screen. It opens the bookmark’s own
edition at the bookmarked page when the edition is downloaded or the
device is online. Otherwise it returns a [`PSEBookmarksEdition`](/documentation/PSReader/PSEBookmarksEdition) built
from the saved copies, one page per bookmark. Show the result in your
reader screen:

```swift
let (source, openingPage) = try await bookmark.editionSource()

let reader = UINavigationController(
    rootViewController: ReaderScreenViewController(source: source, openingPage: openingPage)
)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

The offline edition holds every saved bookmark, so the user can page
between them. To narrow it, for example to one publication, pass the
bookmarks it should hold as `among`, including the one you’re opening.
[`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID) holds the publication GUID; it’s empty
on editions resolved from an edition GUID, such as search results (see
[Identifiers](/documentation/PSReader/Identifiers)):

```swift
let fromThisPublication = PSEBookmarkManager.shared.bookmarks.filter {
    $0.published?.applicationGUID == "PUBLICATION_GUID"
}
let (source, openingPage) = try await bookmark.editionSource(among: fromThisPublication)
```

Pass [`PSEBookmarkOpenMode.alwaysBookmarksEdition`](/documentation/PSReader/PSEBookmarkOpenMode/alwaysBookmarksEdition) as `mode` to show the
saved copies without using the network.

Nothing checks entitlement when a bookmark opens. If you gate editions,
check before you open the bookmark’s own edition; see
[Gating Bookmarks](/documentation/PSReader/Gating-Editions-Behind-a-Paywall#Gating-Bookmarks).

## Observing Changes

The manager reports every bookmark added or removed, whoever made the
change. Use it on the main thread; its callbacks arrive there too.

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkObserver`` has a callback for each kind of change, all
  with empty defaults, so implement only the ones you need. Register with
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/addObserver(_:)``; the manager holds observers
  weakly.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/bookmarksDidChange`` is a notification posted after
  any change, for UI that simply reloads, like the button above.
- In SwiftUI, observe the manager itself: it’s an `ObservableObject`.

## Removing Bookmarks

Removing a bookmark also deletes its saved copy of the content.

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeBookmark(_:)-5vc38`` removes a
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmark`` of either kind, which suits a saved-items list.
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeBookmark(_:page:)`` takes an article record,
  and ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeBookmark(_:)-7ae9a`` a page record.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeBookmark(forArticle:page:)`` and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeBookmark(forPage:)`` remove the bookmark for
  an article or page you have in hand. They do nothing if it isn’t
  bookmarked.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeAllBookmarks()`` removes everything, for
  example when the user signs out.

## Migrating Bookmarks From the Legacy SDK

A custom UI that replaces the legacy SDK can turn the pages its users
saved for offline reading into page bookmarks: call
[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)) once at
startup. Each migrated bookmark is a [`PSEBookmarkPage`](/documentation/PSReader/PSEBookmarkPage) whose
[`isBridged`](/documentation/PSReader/PSEBookmarkPage/isBridged) is `true`; open its edition with
[`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition). Bookmarks made with the legacy SDK don’t
carry over.

[Keeping Users’ Data](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#Keeping-Users-Data) covers when to
call it, opening migrated bookmarks at their page, and customizing the
migration.

## Topics

### Saving Bookmarks

[`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager)

Saves and restores the user’s article and page bookmarks.

### Listing and Opening Bookmarks

[`PSEBookmark`](/documentation/PSReader/PSEBookmark)

A saved bookmark: either an article or a whole page.

[`PSEBookmarkArticle`](/documentation/PSReader/PSEBookmarkArticle)

A persisted article bookmark, carrying the article and its origin so a bookmarks edition can rebuild it offline.

[`PSEBookmarkPage`](/documentation/PSReader/PSEBookmarkPage)

A persisted page bookmark, carrying the page and its origin so a bookmarks edition can rebuild it offline.

[`PSEBookmarkOpenMode`](/documentation/PSReader/PSEBookmarkOpenMode)

How a bookmark should resolve to an edition source when opened.

### Observing Changes

[`PSEBookmarkObserver`](/documentation/PSReader/PSEBookmarkObserver)

Receives bookmark additions and removals from [`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager).

