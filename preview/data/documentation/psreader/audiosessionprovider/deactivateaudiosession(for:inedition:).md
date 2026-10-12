<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioSessionProvider/deactivateAudioSession(for:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20AudioSessionProviderP010deactivatebC03for9inEditionyAA10PSEArticleC_AA16PSEEditionSource_ptKF"
  },
  "title" : "deactivateAudioSession(for:inEdition:)"
}
-->

# deactivateAudioSession(for:inEdition:)

Deactivates the audio session.

```
func deactivateAudioSession(for article: PSEArticle, inEdition source: PSEEditionSource) throws
```

## Parameters

`article`

The text to convert to speech.

`source`

The edition containing the article.

## Discussion

This method should deactivate the audio session when audio playback ends
or is no longer needed. It’s called during cleanup operations.

> Throws: An error if the audio session cannot be deactivated.