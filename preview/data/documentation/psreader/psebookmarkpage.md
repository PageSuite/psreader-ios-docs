<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkPage",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEBookmarkPage"
  },
  "title" : "PSEBookmarkPage"
}
-->

# PSEBookmarkPage

A persisted page bookmark, carrying the page and its origin so a bookmarks edition can rebuild it offline.

```
@objc class PSEBookmarkPage
```

## Topics

### Showing a List Row

[`page`](/documentation/PSReader/PSEBookmarkPage/page)

The saved page.

[`localThumbnailURL()`](/documentation/PSReader/PSEBookmarkPage/localThumbnailURL())

The locally cached page screenshot in the shared saved-bookmarks folder, if
present. Populated for normal bookmarks by `cacheBookmarked(page:)` and for
bridged bookmarks by the page migration; the Saved cell prefers it.

[`remoteLegacyThumbnailURL()`](/documentation/PSReader/PSEBookmarkPage/remoteLegacyThumbnailURL())

Remote legacy page image (the old backend’s page.jpg), used as the Saved-cell
thumbnail fallback for bridged bookmarks — their legacy edition GUID 404s on
the new render endpoint. `page.pageguid` is the legacy page id.

[`editionName`](/documentation/PSReader/PSEBookmarkPage/editionName)

The name of the edition the page was saved from.

[`bookmarkDate`](/documentation/PSReader/PSEBookmarkPage/bookmarkDate)

The edition’s date as display text, copied from the edition when the
page was bookmarked.

[`bookmarkLogo`](/documentation/PSReader/PSEBookmarkPage/bookmarkLogo)

The publication’s header logo for the edition’s date, as set in the
app configuration.

[`dateAdded`](/documentation/PSReader/PSEBookmarkPage/dateAdded)

When the page was bookmarked.

### Source Edition

[`published`](/documentation/PSReader/PSEBookmarkPage/published)

The catalog entry of the edition the page was saved from.

[`editionGUID`](/documentation/PSReader/PSEBookmarkPage/editionGUID)

The GUID of the edition the page was saved from.

[`editionDate`](/documentation/PSReader/PSEBookmarkPage/editionDate)

The publication date of the edition the page was saved from.

### Migrated Bookmarks

[`isBridged`](/documentation/PSReader/PSEBookmarkPage/isBridged)

Whether this bookmark was created by
[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)) from a page
saved with the legacy SDK.

