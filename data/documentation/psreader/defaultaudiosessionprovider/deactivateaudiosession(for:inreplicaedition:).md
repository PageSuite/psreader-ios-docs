<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultAudioSessionProvider/deactivateAudioSession(for:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultAudioSessionProviderV010deactivatecD03for16inReplicaEditionyAA9PSArticleC_AA09PSReplicaJ0VtKF"
  },
  "title" : "deactivateAudioSession(for:inReplicaEdition:)"
}
-->

# deactivateAudioSession(for:inReplicaEdition:)

Deactivates the audio session.

```
func deactivateAudioSession(for article: PSArticle, inReplicaEdition replicaEdition: PSReplicaEdition) throws
```

## Discussion

Deactivates the shared audio session, allowing other apps to take control of audio if needed.