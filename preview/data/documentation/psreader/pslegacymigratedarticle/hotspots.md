<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigratedArticle/hotspots",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PSLegacyMigratedArticleV8hotspotsSayAA0bD7HotspotVGvp"
  },
  "title" : "hotspots"
}
-->

# hotspots

Tappable regions on replica pages that open this article — an article
typically has several. One ARTICLE overlay per hotspot. Empty → the source
falls back to the popover rect, then to cached pxml ARTICLE hotspots.

```
var hotspots: [PSLegacyArticleHotspot]
```