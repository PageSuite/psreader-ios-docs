<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaOverlay",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaOverlay"
  },
  "title" : "PSEMediaOverlay"
}
-->

# PSEMediaOverlay

A view the reader lays over a page’s media hotspot region.

```
@MainActor class PSEMediaOverlay
```

## Overview

The reader positions and sizes overlays to match their hotspot; a
[`PSEditionReaderViewController.MediaDelegate`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol) chooses which overlay (if
any) each hotspot gets. Subclass to draw custom affordances or handle
taps yourself; the base class applies the hotspot’s configured background
and border.

To choose overlays in your own reader screen, see
[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps); in the prebuilt reader, see
[Media and Links](/documentation/PSReader/Media-and-Links).

## Topics

### Creating an Overlay

[`init(page:mediaObject:)`](/documentation/PSReader/PSEMediaOverlay/init(page:mediaObject:))

Creates an overlay for a hotspot, applying the hotspot’s background
and border.

### Hotspot

[`mediaObject`](/documentation/PSReader/PSEMediaOverlay/mediaObject)

The hotspot this overlay covers.

[`page`](/documentation/PSReader/PSEMediaOverlay/page)

The page hosting the hotspot.

### Responding to Visibility

[`isInView()`](/documentation/PSReader/PSEMediaOverlay/isInView())

Called when the overlay’s page becomes the current page.

[`isOutOfView()`](/documentation/PSReader/PSEMediaOverlay/isOutOfView())

Called when the overlay’s page stops being the current page.

