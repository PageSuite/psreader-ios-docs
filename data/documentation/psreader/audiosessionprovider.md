<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioSessionProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20AudioSessionProviderP"
  },
  "title" : "AudioSessionProvider"
}
-->

# AudioSessionProvider

Protocol for managing audio session lifecycle and interruption handling.

```
protocol AudioSessionProvider
```

## Overview

Implementations of this protocol handle the setup, activation, and deactivation of
audio sessions.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultAudioSessionProvider``

## Topics

### Managing the Audio Session

[`setupAudioSession(for:inEdition:)`](/documentation/PSReader/AudioSessionProvider/setupAudioSession(for:inEdition:))

Sets up and activates the audio session for playback.

[`deactivateAudioSession(for:inEdition:)`](/documentation/PSReader/AudioSessionProvider/deactivateAudioSession(for:inEdition:))

Deactivates the audio session.

### Replica Editions

[`setupAudioSession(for:inReplicaEdition:)`](/documentation/PSReader/AudioSessionProvider/setupAudioSession(for:inReplicaEdition:))

Sets up and activates the audio session for replica article playback.

[`deactivateAudioSession(for:inReplicaEdition:)`](/documentation/PSReader/AudioSessionProvider/deactivateAudioSession(for:inReplicaEdition:))

Deactivates the audio session for replica article playback.

