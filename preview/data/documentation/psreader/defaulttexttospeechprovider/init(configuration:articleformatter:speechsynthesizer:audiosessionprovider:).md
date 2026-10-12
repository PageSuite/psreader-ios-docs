<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider/init(configuration:articleFormatter:speechSynthesizer:audioSessionProvider:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC13configuration16articleFormatter17speechSynthesizer012audioSessionF0AcA25AudioOverlayConfigurationV_AA0cde7ArticleI0_pAA0cdeK0_pAA0nmF0_ptcfc"
  },
  "title" : "init(configuration:articleFormatter:speechSynthesizer:audioSessionProvider:)"
}
-->

# init(configuration:articleFormatter:speechSynthesizer:audioSessionProvider:)

Creates a new text-to-speech provider with customizable components.

```
init(configuration: AudioOverlayConfiguration, articleFormatter: any TextToSpeechArticleFormatter = DefaultTextToSpeechArticleFormatter(), speechSynthesizer: any TextToSpeechSynthesizer = DefaultTextToSpeechSynthesizer(), audioSessionProvider: any AudioSessionProvider = DefaultAudioSessionProvider())
```

## Parameters

`configuration`

Visual configuration for the audio overlay interface.

`articleFormatter`

Formatter for preparing article text for speech synthesis.
Defaults to `DefaultTextToSpeechArticleFormatter`.

`speechSynthesizer`

Synthesizer for converting text to speech audio.
Defaults to `DefaultTextToSpeechSynthesizer`.

`audioSessionProvider`

Provides audio session handling.
Defaults to `DefaultAudioSessionProvider`.