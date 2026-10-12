<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/WebReaderShareProvider/isShareable(spread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22WebReaderShareProviderC11isShareable6spread16inReplicaEditionSbAA19PSReplicaPageSpreadO_AA0lK0VtF"
  },
  "title" : "isShareable(spread:inReplicaEdition:)"
}
-->

# isShareable(spread:inReplicaEdition:)

Determines shareability for replica page spreads.
Always `true`: pages link to the replica web reader, and articles to
their article view there.

```
func isShareable(spread: PSReplicaPageSpread, inReplicaEdition replicaEdition: PSReplicaEdition) -> Bool
```