<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider/playAudio(forSpread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC9playAudio9forSpread16inReplicaEditionAA0H7OverlayCSgAA013PSReplicaPageJ0O_AA0oM0VtF"
  },
  "title" : "playAudio(forSpread:inReplicaEdition:)"
}
-->

# playAudio(forSpread:inReplicaEdition:)

Creates and returns an audio overlay for a replica article spread.

```
func playAudio(forSpread spread: PSReplicaPageSpread, inReplicaEdition replicaEdition: PSReplicaEdition) -> AudioOverlay?
```

## Parameters

`spread`

The spread containing the article to play.

`replicaEdition`

The replica edition containing the spread.

## Return Value

An `AudioOverlay` ready for presentation, or `nil` if the spread
is not an article.

## Discussion

This method creates a complete audio interface as a transient overlay.
The overlay includes playback controls, progress indicators, and article
information, all styled according to the provider’s configuration.