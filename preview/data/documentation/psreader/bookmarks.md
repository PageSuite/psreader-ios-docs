<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Bookmarks",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Bookmarks"
}
-->

# Bookmarks

Let users save articles and pages from the prebuilt reader, and reopen them from a Bookmarks screen, even offline.

## Overview

The prebuilt reader has a bookmark button in its navigation bar, and a
Bookmarks screen lists what the user saved. Each bookmark keeps its own
copy of the content, so it reopens without a network connection.
Building a custom UI? See [Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button).

The bookmark button needs no setup. To give users a place to find what
they saved, add the Bookmarks screen to the carousel as a section, or as
a subsection beside your downloads:

```swift
let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE"),
        .section(.init(name: "Bookmarks", type: .bookmarks(type: .all)))
    ]
)
```

![The bookmarks screen listing saved pages and articles.](images/com.pagesuite.PSReader/bookmarks-screen@2x.png)

The reader’s bookmark button appears whenever the page on screen has
something to bookmark ([Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button) lists what each
kind of page saves), and is highlighted once it’s saved. On a
double-page spread, one tap saves both pages, or removes both when both
are saved.

The Bookmarks screen lists saved articles and pages, most recently saved
first. Tapping one opens its edition at the bookmarked page when the
edition is downloaded or the device is online; an edition that isn’t
downloaded streams, even with “Download while reading” on. Offline with
no download, the screen opens the saved copies instead, and the user can
page through every saved item. The bookmark icon on an item removes it.

In the carousel, the section’s ribbon has a menu that sorts the list by
save date or edition date, and deletes every bookmark after asking. The
menu appears in a section whose first subsection is Bookmarks or
Downloads.

Every screen shares one store of bookmarks, so a bookmark saved in one
reader shows up on every Bookmarks screen.

## Showing Bookmarks in Your Own Navigation

[`BookmarksViewController`](/documentation/PSReader/BookmarksViewController) is the same Bookmarks screen for your own
navigation. Outside the carousel it has no menu, so give it a sort
control of your own through
[`sortMode`](/documentation/PSReader/BookmarksViewController/sortMode-swift.property). The chosen order
persists across launches.

```swift
let bookmarks = BookmarksViewController(globalConfig: globalConfig, type: .all)
bookmarks.title = "Bookmarks"
bookmarks.navigationItem.rightBarButtonItem = UIBarButtonItem(
    image: UIImage(systemName: "arrow.up.arrow.down"),
    menu: UIMenu(children: [
        UIAction(title: "Recently Saved") { [weak bookmarks] _ in
            bookmarks?.sortMode = .byBookmarked
        },
        UIAction(title: "Edition Date") { [weak bookmarks] _ in
            bookmarks?.sortMode = .byDate
        }
    ])
)

navigationController?.pushViewController(bookmarks, animated: true)
```

If a container of yours covers part of the screen, such as a custom tab
bar, set [`additionalSafeAreaInsets`](/documentation/PSReader/BookmarksViewController/additionalSafeAreaInsets) to keep the
list clear of it.

[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController) has the same bookmark button as the
carousel’s reader, and the screen shows bookmarks saved there as they’re
made.

## Configuring the Bookmarks Screen

The content type says which bookmarks the screen lists:
[`feedArticle`](/documentation/PSReader/BookmarksConfiguration/BookmarkType/feedArticle) and
[`feedPage`](/documentation/PSReader/BookmarksConfiguration/BookmarkType/feedPage) for articles and pages
saved from editions on the current system, or `.all` for every kind.
Pass it as `type`, in the carousel or to [`BookmarksViewController`](/documentation/PSReader/BookmarksViewController).

A [`BookmarksConfiguration`](/documentation/PSReader/BookmarksConfiguration) styles the screen and sets up the reader it
opens bookmarks in. Pass one as `config` in the carousel, or as
`bookmarksConfig` to [`BookmarksViewController`](/documentation/PSReader/BookmarksViewController). Its
[`readerConfig`](/documentation/PSReader/BookmarksConfiguration/readerConfig) starts with copies of your global
configuration’s delegates; change it to set up that reader alone:

```swift
var bookmarksConfig = BookmarksConfiguration(globalConfig: globalConfig)
bookmarksConfig.bookmarkedIconColor = .systemOrange
bookmarksConfig.readerConfig.shareDelegate = ShareProvider(sharePolicy: .disabled)

let bookmarks = BookmarksViewController(
    globalConfig: globalConfig,
    bookmarksConfig: bookmarksConfig,
    type: [.feedArticle, .feedPage]
)
```

[Theming](/documentation/PSReader/Theming) covers the screen’s colors, labels, and empty state.

The screen opens bookmarks without asking your paywall delegate; see
[Where the Prebuilt UI Asks](/documentation/PSReader/Paywalls#Where-the-Prebuilt-UI-Asks).

> Replica: The Bookmarks screen also lists bookmarks saved from replica
> editions when its type includes
> ``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksConfiguration/BookmarkType/replicaPage`` or
> ``doc://com.pagesuite.PSReader/documentation/PSReader/BookmarksConfiguration/BookmarkType/replicaArticle``, as `.all` does,
> and opens them in the replica reader.

## Removing Bookmarks

The prebuilt UI keeps its bookmarks in [`PSEBookmarkManager`](/documentation/PSReader/PSEBookmarkManager), so your
code can reach them. To remove every bookmark when a user signs out:

```swift
PSEBookmarkManager.shared.removeAllBookmarks()
```

In the prebuilt reader, the settings menu’s “Clear edition data” row
removes every bookmark along with the downloads; see
[Download Settings in the Prebuilt Reader](/documentation/PSReader/Downloads-and-Offline-Reading#Download-Settings-in-the-Prebuilt-Reader).
[Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button) covers the rest of the manager: listing
and opening saved items, and observing changes.

> Replica: ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager`` doesn’t hold replica bookmarks, which
> the legacy replica system keeps, so
> ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEBookmarkManager/removeAllBookmarks()`` leaves them in place.

## Bookmarks From the Legacy SDK

The prebuilt Bookmarks screen lists the legacy SDK’s bookmarks itself,
as replica content, when its type includes replica bookmarks, and opens
them in the replica reader. Apps that use the prebuilt screens leave out
[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)), the custom
UI’s migration call. Pages saved for offline reading with the legacy SDK
have no prebuilt screen. See
[With the Prebuilt Screens](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK#With-the-Prebuilt-Screens).

## Topics

### Showing Bookmarks

[`BookmarksViewController`](/documentation/PSReader/BookmarksViewController)

A standalone view controller for displaying bookmarked pages and articles.

### Configuring the Bookmarks Screen

[`BookmarksConfiguration`](/documentation/PSReader/BookmarksConfiguration)

Configuration for customizing the appearance and behavior of bookmark archives.

