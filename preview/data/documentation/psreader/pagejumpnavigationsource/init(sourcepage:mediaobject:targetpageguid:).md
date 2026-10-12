<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PageJumpNavigationSource/init(sourcePage:mediaObject:targetPageGUID:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24PageJumpNavigationSourceV06sourceB011mediaObject06targetB4GUIDAcA7PSEPageCSg_AA08PSEMediaH0CSgSStcfc"
  },
  "title" : "init(sourcePage:mediaObject:targetPageGUID:)"
}
-->

# init(sourcePage:mediaObject:targetPageGUID:)

Creates a page-jump token.

```
init(sourcePage: PSEPage? = nil, mediaObject: PSEMediaObject? = nil, targetPageGUID: String)
```

## Parameters

`sourcePage`

The page whose content triggered the jump.

`mediaObject`

The hotspot that triggered the jump, if any.

`targetPageGUID`

The GUID of the page the jump targets.

## Discussion

The reader creates these for its own jumps. Create one yourself only
to pass as the `source` of a `scrollTo` call, so your
[`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) handles a jump you
trigger the same way as the reader’s.