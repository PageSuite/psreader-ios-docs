<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioDelegate/playAudio(forSpread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AudioDelegateP04playB09forSpread16inReplicaEditionAA0B7OverlayCSgAA013PSReplicaPageF0O_AA0kI0VtF"
  },
  "title" : "playAudio(forSpread:inReplicaEdition:)"
}
-->

# playAudio(forSpread:inReplicaEdition:)

Provides a transient audio overlay for the specified replica spread.

```
func playAudio(forSpread spread: PSReplicaPageSpread, inReplicaEdition replicaEdition: PSReplicaEdition) -> AudioOverlay?
```

## Parameters

`spread`

The spread for which audio playback is requested.

`replicaEdition`

The replica edition containing the spread.

## Return Value

An `AudioOverlay` subclass for presenting audio controls,
or `nil` if no overlay should be shown.

## Discussion

This method should return an `AudioOverlay` subclass that will be presented
as a popover-style interface for audio playback. The overlay is typically
triggered by user interaction and provides focused audio controls.

The default implementation returns `nil`.