<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigratedArticle/init(legacyArticle:html:articleMetadata:imageURLsToMaterialize:hotspots:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PSLegacyMigratedArticleV06legacyD04html15articleMetadata22imageURLsToMaterialize8hotspotsAcA9PSArticleC_SSSDySSypGSaySSGSayAA0bD7HotspotVGtcfc"
  },
  "title" : "init(legacyArticle:html:articleMetadata:imageURLsToMaterialize:hotspots:)"
}
-->

# init(legacyArticle:html:articleMetadata:imageURLsToMaterialize:hotspots:)

Creates an article page for a migrated edition.

```
init(legacyArticle: PSArticle, html: String, articleMetadata: [String : Any] = [:], imageURLsToMaterialize: [String] = [], hotspots: [PSLegacyArticleHotspot] = [])
```

## Parameters

`legacyArticle`

The legacy article the page presents.

`html`

The page’s complete HTML.

`articleMetadata`

Extra article fields, applied over the ones
taken from `legacyArticle`.

`imageURLsToMaterialize`

Legacy image URLs to copy into the edition
folder.

`hotspots`

The regions on the edition’s PDF pages that open the
article.