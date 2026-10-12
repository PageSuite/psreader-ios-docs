<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultAudioSessionProvider/setupAudioSession(for:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultAudioSessionProviderV05setupcD03for16inReplicaEditionyAA9PSArticleC_AA09PSReplicaJ0VtKF"
  },
  "title" : "setupAudioSession(for:inReplicaEdition:)"
}
-->

# setupAudioSession(for:inReplicaEdition:)

Sets up audio session for playback with background capability.

```
func setupAudioSession(for article: PSArticle, inReplicaEdition replicaEdition: PSReplicaEdition) throws
```

## Discussion

Configures the audio session category to `.playback` with default mode
and activates the session for audio playback.