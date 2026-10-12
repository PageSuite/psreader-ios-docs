<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC"
  },
  "title" : "DefaultTextToSpeechProvider"
}
-->

# DefaultTextToSpeechProvider

A complete text-to-speech implementation providing ready-to-use audio functionality.

```
class DefaultTextToSpeechProvider
```

## Overview

`DefaultTextToSpeechProvider` implements the [`AudioDelegate`](/documentation/PSReader/AudioDelegate) protocol with full
text-to-speech capabilities using the SDK’s built-in components. This provider
offers a complete solution for adding TTS functionality to your publication reader.

The provider handles:

- Article text formatting for optimal speech synthesis
- Text-to-speech conversion using system or custom synthesizers
- Audio playback with an elegant overlay interface
- Automatic content management and state tracking

This implementation is designed for single-article pages and provides sensible
defaults that work well for most use cases while allowing customization of
formatters, synthesizers, and visual styling.

## Usage

```swift
let config = AudioOverlayConfiguration(globalConfig: globalConfig)
let ttsProvider = DefaultTextToSpeechProvider(configuration: config)

var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
globalConfig.audioDelegate = ttsProvider
```

Each component can be replaced independently for advanced use cases:

```swift
let ttsProvider = DefaultTextToSpeechProvider(
    configuration: config,
    articleFormatter: MyCustomFormatter(),
    speechSynthesizer: MyCloudTTSSynthesizer(),
    audioSessionProvider: DefaultAudioSessionProvider()
)
```

Building your own reader screen? [Adding a Listen Button](/documentation/PSReader/Adding-a-Listen-Button) drives the
same provider from your own button.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechArticleFormatter``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechSynthesizer``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioSessionProvider``

## Topics

### Creating a Provider

[`init(configuration:articleFormatter:speechSynthesizer:audioSessionProvider:)`](/documentation/PSReader/DefaultTextToSpeechProvider/init(configuration:articleFormatter:speechSynthesizer:audioSessionProvider:))

Creates a new text-to-speech provider with customizable components.

### Playing an Article

[`isListenable(page:inEdition:)`](/documentation/PSReader/DefaultTextToSpeechProvider/isListenable(page:inEdition:))

Determines if a page can be read aloud using text-to-speech.

[`playAudio(for:inEdition:)`](/documentation/PSReader/DefaultTextToSpeechProvider/playAudio(for:inEdition:))

Creates and returns an audio overlay for the specified page.

[`didChangeTo(page:inEdition:inPublished:)`](/documentation/PSReader/DefaultTextToSpeechProvider/didChangeTo(page:inEdition:inPublished:))

Handles page navigation by managing audio player state.

### Showing a Banner

[`audioBannerViewController()`](/documentation/PSReader/DefaultTextToSpeechProvider/audioBannerViewController())

Returns the persistent banner view controller.

### Replica Editions

[`isListenable(spread:inReplicaEdition:)`](/documentation/PSReader/DefaultTextToSpeechProvider/isListenable(spread:inReplicaEdition:))

Determines if a replica spread can be read aloud using text-to-speech.

[`playAudio(forSpread:inReplicaEdition:)`](/documentation/PSReader/DefaultTextToSpeechProvider/playAudio(forSpread:inReplicaEdition:))

Creates and returns an audio overlay for a replica article spread.

[`didChangeTo(spread:inReplicaEdition:)`](/documentation/PSReader/DefaultTextToSpeechProvider/didChangeTo(spread:inReplicaEdition:))

Handles replica spread navigation by managing audio player state.

