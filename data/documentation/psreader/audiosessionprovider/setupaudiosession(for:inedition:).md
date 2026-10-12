<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioSessionProvider/setupAudioSession(for:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20AudioSessionProviderP05setupbC03for9inEditionyAA10PSEArticleC_AA16PSEEditionSource_ptKF"
  },
  "title" : "setupAudioSession(for:inEdition:)"
}
-->

# setupAudioSession(for:inEdition:)

Sets up and activates the audio session for playback.

```
func setupAudioSession(for article: PSEArticle, inEdition source: PSEEditionSource) throws
```

## Parameters

`article`

The text to convert to speech.

`source`

The edition containing the article.

## Discussion

This method should configure the audio session category (typically `.playback`)
and activate the session. It’s called when audio playback begins.

> Throws: An error if the audio session cannot be configured or activated.