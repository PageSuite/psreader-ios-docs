<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider/didChangeTo(spread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC09didChangeD06spread16inReplicaEditionyAA19PSReplicaPageSpreadOSg_AA0mL0VtF"
  },
  "title" : "didChangeTo(spread:inReplicaEdition:)"
}
-->

# didChangeTo(spread:inReplicaEdition:)

Handles replica spread navigation by managing audio player state.

```
func didChangeTo(spread: PSReplicaPageSpread?, inReplicaEdition replicaEdition: PSReplicaEdition)
```

## Parameters

`spread`

The new spread being displayed, or `nil` if no specific spread is active.

`replicaEdition`

The replica edition containing the spread.

## Discussion

When the user navigates to a different spread, this method checks if the
currently playing audio corresponds to the new spread. If not, it clears
the current player to stop playback and free resources.