<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyArticleHotspot",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyArticleHotspotV"
  },
  "title" : "PSLegacyArticleHotspot"
}
-->

# PSLegacyArticleHotspot

One tappable region for an article on a replica page. Coordinates are percent
of the page, origin top-left — the same space as legacy pxml hotspots.

```
struct PSLegacyArticleHotspot
```

## Topics

### Creating a Hotspot

[`init(pageNumber:rect:)`](/documentation/PSReader/PSLegacyArticleHotspot/init(pageNumber:rect:))

Creates a hotspot.

### Region

[`pageNumber`](/documentation/PSReader/PSLegacyArticleHotspot/pageNumber)

The number of the PDF page the region is on, counting from 1.

[`rect`](/documentation/PSReader/PSLegacyArticleHotspot/rect)

The region, in percent of the page’s width and height, with the
origin at the top left. Empty regions are ignored.

