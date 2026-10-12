<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AudioDelegateP"
  },
  "title" : "AudioDelegate"
}
-->

# AudioDelegate

Delegate protocol used to provide audio playback functionality within the SDK.

```
protocol AudioDelegate
```

## Overview

The AudioDelegate protocol enables text-to-speech and other audio features for publication content.
Implementations can provide either a persistent banner interface or transient overlay interface,
or both approaches depending on the user experience requirements.

There are two primary audio interface patterns supported:

- **Persistent Banner**: Return a banner view controller from ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/audioBannerViewController()`` and
  control its visibility using intrinsic content size (zero height hides the banner).
- **Transient Overlay**: Return a subclass of ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlay`` from ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/playAudio(for:inEdition:)``
  which functions as a popover-style interface.

## Quick Start

Use [`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider) for a ready-to-use TTS implementation:

```swift
let config = AudioOverlayConfiguration(globalConfig: globalConfig)
let ttsProvider = DefaultTextToSpeechProvider(configuration: config)

var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
globalConfig.audioDelegate = ttsProvider
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechProvider``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlay``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioBannerViewController``

## Topics

### Playing an Article

[`isListenable(page:inEdition:)`](/documentation/PSReader/AudioDelegate/isListenable(page:inEdition:))

Determines if a page within an edition supports audio playback.

[`playAudio(for:inEdition:)`](/documentation/PSReader/AudioDelegate/playAudio(for:inEdition:))

Provides a transient audio overlay for the specified page.

[`didChangeTo(page:inEdition:inPublished:)`](/documentation/PSReader/AudioDelegate/didChangeTo(page:inEdition:inPublished:))

Called when the user navigates to a different page.

### Showing a Banner

[`audioBannerViewController()`](/documentation/PSReader/AudioDelegate/audioBannerViewController())

Provides a persistent banner view controller for audio controls.

### Replica Editions

[`isListenable(spread:inReplicaEdition:)`](/documentation/PSReader/AudioDelegate/isListenable(spread:inReplicaEdition:))

Determines if a replica spread supports audio playback.

[`playAudio(forSpread:inReplicaEdition:)`](/documentation/PSReader/AudioDelegate/playAudio(forSpread:inReplicaEdition:))

Provides a transient audio overlay for the specified replica spread.

[`didChangeTo(spread:inReplicaEdition:)`](/documentation/PSReader/AudioDelegate/didChangeTo(spread:inReplicaEdition:))

Called when the user navigates to a different replica spread.

