<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SectionJumpNavigationSource/mediaObject",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27SectionJumpNavigationSourceV11mediaObjectAA08PSEMediaG0CSgvp"
  },
  "title" : "mediaObject"
}
-->

# mediaObject

The hotspot that triggered the jump, or `nil` when the jump didn’t
come from a hotspot. The reader’s own section jumps come from links
in templated pages, so they leave this `nil`.

```
let mediaObject: PSEMediaObject?
```