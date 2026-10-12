<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioOverlay",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)AudioOverlay"
  },
  "title" : "AudioOverlay"
}
-->

# AudioOverlay

A custom view controller designed for presenting audio playback interfaces as overlays.

```
@MainActor class AudioOverlay
```

## Overview

`AudioOverlay` serves as the base class for transient audio interfaces that are presented
as popover-style overlays. Subclass this view controller to create custom audio playback
interfaces that integrate seamlessly with the SDK’s presentation system.

The overlay automatically manages its lifecycle and coordinates with the SDK’s overlay
management system to ensure proper presentation and dismissal animations.

When creating a custom audio overlay:

1. Subclass `AudioOverlay`
1. Design your audio interface in the subclass
1. Return an instance from ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/playAudio(for:inEdition:)``

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate``

## Topics

### Highlighting the Listen Button

[`viewWillAppear(_:)`](/documentation/PSReader/AudioOverlay/viewWillAppear(_:))

Highlights the reader’s navigation bar button for the overlay when the
reader presents the overlay as a popover.

[`viewWillDisappear(_:)`](/documentation/PSReader/AudioOverlay/viewWillDisappear(_:))

Removes the highlight from the reader’s navigation bar button for the
overlay when the reader dismisses the overlay from a popover.

