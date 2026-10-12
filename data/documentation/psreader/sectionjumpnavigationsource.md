<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SectionJumpNavigationSource",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27SectionJumpNavigationSourceV"
  },
  "title" : "SectionJumpNavigationSource"
}
-->

# SectionJumpNavigationSource

The scroll-source token the reader passes when in-page content (a
section link or media hotspot) triggers a jump to a section.

```
struct SectionJumpNavigationSource
```

## Topics

### Reading the Jump

[`targetSectionGUID`](/documentation/PSReader/SectionJumpNavigationSource/targetSectionGUID)

The section the jump targets, matched as
[`scrollTo(sectionGUID:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(sectionGUID:source:))
matches it.

[`sourcePage`](/documentation/PSReader/SectionJumpNavigationSource/sourcePage)

The page whose content triggered the jump, or `nil` when unknown.

[`mediaObject`](/documentation/PSReader/SectionJumpNavigationSource/mediaObject)

The hotspot that triggered the jump, or `nil` when the jump didn’t
come from a hotspot. The reader’s own section jumps come from links
in templated pages, so they leave this `nil`.

### Tagging Your Own Jumps

[`init(sourcePage:mediaObject:targetSectionGUID:)`](/documentation/PSReader/SectionJumpNavigationSource/init(sourcePage:mediaObject:targetSectionGUID:))

Creates a section-jump token.

