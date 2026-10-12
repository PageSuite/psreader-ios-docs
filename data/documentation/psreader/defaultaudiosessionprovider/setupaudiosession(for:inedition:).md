<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultAudioSessionProvider/setupAudioSession(for:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultAudioSessionProviderV05setupcD03for9inEditionyAA10PSEArticleC_AA16PSEEditionSource_ptKF"
  },
  "title" : "setupAudioSession(for:inEdition:)"
}
-->

# setupAudioSession(for:inEdition:)

Sets up audio session for playback with background capability.

```
func setupAudioSession(for article: PSEArticle, inEdition source: PSEEditionSource) throws
```

## Discussion

Configures the audio session category to `.playback` with default mode
and activates the session for audio playback.