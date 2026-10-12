<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigrationHooks",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyMigrationHooksP"
  },
  "title" : "PSLegacyMigrationHooks"
}
-->

# PSLegacyMigrationHooks

Customizes how content saved with the legacy SDK migrates to the current
SDK.

```
protocol PSLegacyMigrationHooks : AnyObject
```

## Overview

Pass a conforming class to
[`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:)) and
[`migrateLegacyPageBookmarks(hooks:)`](/documentation/PSReader/PSEBookmarkManager/migrateLegacyPageBookmarks(hooks:)). Every
requirement has a default, so implement only what you need to change;
[`PSLegacyDefaultMigrationHooks`](/documentation/PSReader/PSLegacyDefaultMigrationHooks) uses the defaults throughout.

The requirements run at two different times:

- **At migration.** ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/accountGUID``, ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/applicationGUID`` and
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/publicationGUID(forLegacyPublicationGUID:)`` set the identity of the
  catalog entries migration creates for legacy downloads and saved
  pages. For downloads only, ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/shouldMigrate(edition:)`` can leave an
  edition out and ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/retainedLegacyCacheURLs(forEdition:)`` keeps extra
  cached files.
- **When a migrated edition opens.**
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/migratedArticles(forEdition:legacyArticles:context:)`` builds its
  article pages and ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyMigrationHooks/additionalEditionResources(forEdition:)`` supplies
  the files they reference. These run for the hooks passed to
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:completion:)``;
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)`` opens migrated
  editions with ``doc://com.pagesuite.PSReader/documentation/PSReader/PSLegacyDefaultMigrationHooks``.

To move an app from the legacy core SDK, see
[Migrating From the Legacy Core SDK](/documentation/PSReader/Migrating-From-the-Legacy-Core-SDK).

## Topics

### Identifying Migrated Entries

[`accountGUID`](/documentation/PSReader/PSLegacyMigrationHooks/accountGUID)

The account GUID recorded on each catalog entry migration creates, as
its `accountGUID`.

[`applicationGUID`](/documentation/PSReader/PSLegacyMigrationHooks/applicationGUID)

The publication GUID recorded on each catalog entry migration
creates, as its [`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID).

[`publicationGUID(forLegacyPublicationGUID:)`](/documentation/PSReader/PSLegacyMigrationHooks/publicationGUID(forLegacyPublicationGUID:))

Returns the value to record as a migrated catalog entry’s
`publicationGUID`, given the legacy edition’s replica publication
GUID.

### Choosing What Migrates

[`shouldMigrate(edition:)`](/documentation/PSReader/PSLegacyMigrationHooks/shouldMigrate(edition:))

Returns whether to migrate an edition downloaded with the legacy SDK.

[`retainedLegacyCacheURLs(forEdition:)`](/documentation/PSReader/PSLegacyMigrationHooks/retainedLegacyCacheURLs(forEdition:))

Returns the URLs of files your app cached through the legacy SDK for
an edition, such as article feeds, that must stay readable offline
after migration.

### Building Article Pages

[`migratedArticles(forEdition:legacyArticles:context:)`](/documentation/PSReader/PSLegacyMigrationHooks/migratedArticles(forEdition:legacyArticles:context:))

Builds the article pages of a migrated edition from its legacy
articles.

[`additionalEditionResources(forEdition:)`](/documentation/PSReader/PSLegacyMigrationHooks/additionalEditionResources(forEdition:))

Returns extra files, such as stylesheets and fonts, to write into a
migrated edition’s folder for its article HTML to reference.

### Default Hooks and Hook Values

[`PSLegacyDefaultMigrationHooks`](/documentation/PSReader/PSLegacyDefaultMigrationHooks)

Default hooks — the generic behavior with no client identity. A client that
needs identity/article presentation supplies its own conformer.

[`PSLegacyEditionSummary`](/documentation/PSReader/PSLegacyEditionSummary)

Read-only view of a legacy edition handed to hooks.

[`PSLegacyMigratedArticle`](/documentation/PSReader/PSLegacyMigratedArticle)

One article page to fabricate lazily at open, produced by the hooks from a
legacy article.

[`PSLegacyArticleContext`](/documentation/PSReader/PSLegacyArticleContext)

Helpers handed to the hooks while they build migrated articles at open time.
Cache-first with network fallback (the edition is opening; the network layer is
available and self-heals the cache).

[`PSLegacyArticleHotspot`](/documentation/PSReader/PSLegacyArticleHotspot)

One tappable region for an article on a replica page. Coordinates are percent
of the page, origin top-left — the same space as legacy pxml hotspots.

[`PSLegacyEditionResource`](/documentation/PSReader/PSLegacyEditionResource)

A file placed into the edition folder next to the page assets — stylesheets and
fonts the article HTML references by relative name.

