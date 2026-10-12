<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioDelegate/didChangeTo(spread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AudioDelegateP11didChangeTo6spread16inReplicaEditionyAA19PSReplicaPageSpreadOSg_AA0kJ0VtF"
  },
  "title" : "didChangeTo(spread:inReplicaEdition:)"
}
-->

# didChangeTo(spread:inReplicaEdition:)

Called when the user navigates to a different replica spread.

```
func didChangeTo(spread: PSReplicaPageSpread?, inReplicaEdition replicaEdition: PSReplicaEdition)
```

## Parameters

`spread`

The new spread being displayed, or `nil` if no specific spread is active.

`replicaEdition`

The replica edition containing the spread.

## Discussion

Use this method to handle audio state changes when users navigate between spreads.
For example, you might pause current audio playback or update persistent banner state.

Note: A default implementation is provided that does nothing.