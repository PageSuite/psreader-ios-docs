<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SectionJumpNavigationSource/init(sourcePage:mediaObject:targetSectionGUID:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27SectionJumpNavigationSourceV10sourcePage11mediaObject06targetB4GUIDAcA7PSEPageCSg_AA08PSEMediaI0CSgSStcfc"
  },
  "title" : "init(sourcePage:mediaObject:targetSectionGUID:)"
}
-->

# init(sourcePage:mediaObject:targetSectionGUID:)

Creates a section-jump token.

```
init(sourcePage: PSEPage? = nil, mediaObject: PSEMediaObject? = nil, targetSectionGUID: String)
```

## Parameters

`sourcePage`

The page whose content triggered the jump.

`mediaObject`

The hotspot that triggered the jump, if any.

`targetSectionGUID`

The section the jump targets.

## Discussion

The reader creates these for its own jumps. Create one yourself only
to pass as the `source` of a `scrollTo` call, so your
[`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) handles a jump you
trigger the same way as the reader’s.