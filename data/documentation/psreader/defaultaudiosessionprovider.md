<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultAudioSessionProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultAudioSessionProviderV"
  },
  "title" : "DefaultAudioSessionProvider"
}
-->

# DefaultAudioSessionProvider

Default implementation of audio session management.

```
struct DefaultAudioSessionProvider
```

## Overview

This provider offers standard audio session handling using AVAudioSession
with sensible defaults for text-to-speech playback. It configures the session
for background playback and handles interruptions appropriately.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioSessionProvider``

## Topics

### Creating a Provider

[`init()`](/documentation/PSReader/DefaultAudioSessionProvider/init())

Creates a new default audio session provider.

### Managing the Audio Session

[`setupAudioSession(for:inEdition:)`](/documentation/PSReader/DefaultAudioSessionProvider/setupAudioSession(for:inEdition:))

Sets up audio session for playback with background capability.

[`deactivateAudioSession(for:inEdition:)`](/documentation/PSReader/DefaultAudioSessionProvider/deactivateAudioSession(for:inEdition:))

Deactivates the audio session.

### Replica Editions

[`setupAudioSession(for:inReplicaEdition:)`](/documentation/PSReader/DefaultAudioSessionProvider/setupAudioSession(for:inReplicaEdition:))

Sets up audio session for playback with background capability.

[`deactivateAudioSession(for:inReplicaEdition:)`](/documentation/PSReader/DefaultAudioSessionProvider/deactivateAudioSession(for:inReplicaEdition:))

Deactivates the audio session.

