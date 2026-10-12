<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultAudioSessionProvider/deactivateAudioSession(for:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultAudioSessionProviderV010deactivatecD03for9inEditionyAA10PSEArticleC_AA16PSEEditionSource_ptKF"
  },
  "title" : "deactivateAudioSession(for:inEdition:)"
}
-->

# deactivateAudioSession(for:inEdition:)

Deactivates the audio session.

```
func deactivateAudioSession(for article: PSEArticle, inEdition source: PSEEditionSource) throws
```

## Discussion

Deactivates the shared audio session, allowing other apps to take control of audio if needed.