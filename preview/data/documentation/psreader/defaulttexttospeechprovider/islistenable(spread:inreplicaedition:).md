<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider/isListenable(spread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC12isListenable6spread16inReplicaEditionSbAA19PSReplicaPageSpreadO_AA0mL0VtF"
  },
  "title" : "isListenable(spread:inReplicaEdition:)"
}
-->

# isListenable(spread:inReplicaEdition:)

Determines if a replica spread can be read aloud using text-to-speech.

```
func isListenable(spread: PSReplicaPageSpread, inReplicaEdition replicaEdition: PSReplicaEdition) -> Bool
```

## Parameters

`spread`

The spread to evaluate for TTS capability.

`replicaEdition`

The replica edition containing the spread.

## Return Value

`true` if the spread is an article; otherwise, `false`.

## Discussion

Only article spreads are listenable.