<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareDelegate/shareContext(forSpread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareDelegateP12shareContext9forSpread16inReplicaEditionAA0bE0VSgAA013PSReplicaPageG0O_AA0kJ0VtF"
  },
  "title" : "shareContext(forSpread:inReplicaEdition:)"
}
-->

# shareContext(forSpread:inReplicaEdition:)

Provides the sharing context for a replica page spread.

```
func shareContext(forSpread spread: PSReplicaPageSpread, inReplicaEdition replicaEdition: PSReplicaEdition) -> ShareContext?
```

## Parameters

`spread`

The page spread to share.

`replicaEdition`

The replica edition containing the spread.

## Return Value

A `ShareContext` object containing the items to share,
or `nil` if the spread is not shareable.

## Discussion

The default implementation returns `nil`, so a delegate that implements
only the methods for editions on PageSuite’s current system doesn’t
share legacy replica editions.