<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioDelegate/isListenable(spread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AudioDelegateP12isListenable6spread16inReplicaEditionSbAA19PSReplicaPageSpreadO_AA0jI0VtF"
  },
  "title" : "isListenable(spread:inReplicaEdition:)"
}
-->

# isListenable(spread:inReplicaEdition:)

Determines if a replica spread supports audio playback.

```
func isListenable(spread: PSReplicaPageSpread, inReplicaEdition replicaEdition: PSReplicaEdition) -> Bool
```

## Parameters

`spread`

The page spread currently being evaluated.

`replicaEdition`

The replica edition containing the spread.

## Return Value

`true` if the spread supports audio playback; otherwise, `false`.

## Discussion

Use this method to control which spreads display audio controls or functionality.
This is called by the SDK to determine whether to show audio-related UI elements.

The default implementation returns `false`, so a delegate that
implements only the methods for editions on PageSuite’s current system
offers no audio in legacy replica editions.