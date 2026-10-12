<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PageJumpNavigationSource/mediaObject",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24PageJumpNavigationSourceV11mediaObjectAA08PSEMediaG0CSgvp"
  },
  "title" : "mediaObject"
}
-->

# mediaObject

The hotspot that triggered the jump, or `nil` when the jump didn’t
come from a hotspot. The reader tags page jumps from
[`PSEMediaArticleOverlay`](/documentation/PSReader/PSEMediaArticleOverlay) and [`PSEMediaLinkOverlay`](/documentation/PSReader/PSEMediaLinkOverlay) taps, which
set it.

```
let mediaObject: PSEMediaObject?
```