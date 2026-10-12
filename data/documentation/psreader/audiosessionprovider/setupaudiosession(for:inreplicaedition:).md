<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioSessionProvider/setupAudioSession(for:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20AudioSessionProviderP05setupbC03for16inReplicaEditionyAA9PSArticleC_AA09PSReplicaI0VtKF"
  },
  "title" : "setupAudioSession(for:inReplicaEdition:)"
}
-->

# setupAudioSession(for:inReplicaEdition:)

Sets up and activates the audio session for replica article playback.

```
func setupAudioSession(for article: PSArticle, inReplicaEdition replicaEdition: PSReplicaEdition) throws
```

## Parameters

`article`

The replica article to play.

`replicaEdition`

The replica edition containing the article.

## Discussion

The default implementation sets the shared audio session to the
`.playback` category and activates it, as [`DefaultAudioSessionProvider`](/documentation/PSReader/DefaultAudioSessionProvider)
does.

> Throws: An error if the audio session cannot be configured or activated.