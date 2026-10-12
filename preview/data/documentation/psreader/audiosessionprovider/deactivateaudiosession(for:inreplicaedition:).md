<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioSessionProvider/deactivateAudioSession(for:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20AudioSessionProviderP010deactivatebC03for16inReplicaEditionyAA9PSArticleC_AA09PSReplicaI0VtKF"
  },
  "title" : "deactivateAudioSession(for:inReplicaEdition:)"
}
-->

# deactivateAudioSession(for:inReplicaEdition:)

Deactivates the audio session for replica article playback.

```
func deactivateAudioSession(for article: PSArticle, inReplicaEdition replicaEdition: PSReplicaEdition) throws
```

## Parameters

`article`

The replica article.

`replicaEdition`

The replica edition containing the article.

## Discussion

The default implementation deactivates the shared audio session, as
[`DefaultAudioSessionProvider`](/documentation/PSReader/DefaultAudioSessionProvider) does.

> Throws: An error if the audio session cannot be deactivated.