<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioDelegate/playAudio(for:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AudioDelegateP04playB03for9inEditionAA0B7OverlayCSgAA7PSEPageC_AA16PSEEditionSource_ptF"
  },
  "title" : "playAudio(for:inEdition:)"
}
-->

# playAudio(for:inEdition:)

Provides a transient audio overlay for the specified page.

```
func playAudio(for page: PSEPage, inEdition source: PSEEditionSource) -> AudioOverlay?
```

## Parameters

`page`

The page for which audio playback is requested.

`source`

The edition source containing the page.

## Return Value

An `AudioOverlay` subclass for presenting audio controls,
or `nil` if no overlay should be shown.

## Discussion

This method should return an `AudioOverlay` subclass that will be presented
as a popover-style interface for audio playback. The overlay is typically
triggered by user interaction and provides focused audio controls.