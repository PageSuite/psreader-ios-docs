<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaOverlay/init(page:mediaObject:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PSEMediaOverlayC4page11mediaObjectAcA7PSEPageC_AA0bF0Ctcfc"
  },
  "title" : "init(page:mediaObject:)"
}
-->

# init(page:mediaObject:)

Creates an overlay for a hotspot, applying the hotspot’s background
and border.

```
@MainActor init(page: PSEPage, mediaObject: PSEMediaObject)
```

## Parameters

`page`

The page hosting the hotspot.

`mediaObject`

The hotspot to cover.

## Discussion

When `mediaObject.background` is `true` the overlay fills with the
hotspot’s `backgroundColor` at its `backgroundAlpha`; when
`mediaObject.border` is `true` it draws a 1-point border in the
hotspot’s `borderColor` at its `borderAlpha`. The reader sets the
overlay’s frame.