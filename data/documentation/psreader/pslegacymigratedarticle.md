<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigratedArticle",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PSLegacyMigratedArticleV"
  },
  "title" : "PSLegacyMigratedArticle"
}
-->

# PSLegacyMigratedArticle

One article page to fabricate lazily at open, produced by the hooks from a
legacy article.

```
struct PSLegacyMigratedArticle
```

## Topics

### Creating an Article Page

[`init(legacyArticle:html:articleMetadata:imageURLsToMaterialize:hotspots:)`](/documentation/PSReader/PSLegacyMigratedArticle/init(legacyArticle:html:articleMetadata:imageURLsToMaterialize:hotspots:))

Creates an article page for a migrated edition.

### Source Article

[`legacyArticle`](/documentation/PSReader/PSLegacyMigratedArticle/legacyArticle)

The legacy source article. `id`, `pnum` and the x/y/width/height hotspot
coordinates drive the ARTICLE overlay placed on the owning replica page.

### Page Content

[`html`](/documentation/PSReader/PSLegacyMigratedArticle/html)

Render-ready page HTML, loaded verbatim from a file inside the edition
folder — no SDK template processing touches it. Reference materialized
images and edition resources by their edition-folder-relative names (see
`PSLegacyArticleContext.localImageReference(forLegacyURL:)`); absolute
http(s) URLs are also allowed but load online only.

[`articleMetadata`](/documentation/PSReader/PSLegacyMigratedArticle/articleMetadata)

Extra fields merged into the fabricated PSEArticle dictionary on the page
(e.g. “subheadline”, “byline”, “images”). Defaults from `legacyArticle` are
applied first and overridden here.

[`imageURLsToMaterialize`](/documentation/PSReader/PSLegacyMigratedArticle/imageURLsToMaterialize)

Legacy image URLs to copy into the edition folder so the HTML references
them offline by relative filename.

[`hotspots`](/documentation/PSReader/PSLegacyMigratedArticle/hotspots)

Tappable regions on replica pages that open this article — an article
typically has several. One ARTICLE overlay per hotspot. Empty → the source
falls back to the popover rect, then to cached pxml ARTICLE hotspots.

