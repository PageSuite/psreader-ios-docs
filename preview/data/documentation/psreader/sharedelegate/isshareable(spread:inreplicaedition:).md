<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareDelegate/isShareable(spread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareDelegateP11isShareable6spread16inReplicaEditionSbAA19PSReplicaPageSpreadO_AA0jI0VtF"
  },
  "title" : "isShareable(spread:inReplicaEdition:)"
}
-->

# isShareable(spread:inReplicaEdition:)

Determines if a replica page spread is shareable.

```
func isShareable(spread: PSReplicaPageSpread, inReplicaEdition replicaEdition: PSReplicaEdition) -> Bool
```

## Parameters

`spread`

The page spread currently being viewed.

`replicaEdition`

The replica edition containing the spread.

## Return Value

`true` if the spread is shareable; otherwise, `false`.

## Discussion

The default implementation returns whether
[`shareContext(forSpread:inReplicaEdition:)`](/documentation/PSReader/ShareDelegate/shareContext(forSpread:inReplicaEdition:)) returns a context.