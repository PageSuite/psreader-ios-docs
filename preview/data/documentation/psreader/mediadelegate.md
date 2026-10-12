<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/MediaDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13MediaDelegateP"
  },
  "title" : "MediaDelegate"
}
-->

# MediaDelegate

Defines methods to provide custom media functionality.

```
protocol MediaDelegate
```

## Overview

The SDK does **not** include built-in video playback. Implement this delegate
to enable video and interactive media experiences within the reader.

## Usage

```swift
import AVKit

struct MyMediaDelegate: MediaDelegate {
    func videoViewController(
        for video: PSEVideo,
        presentingFrom: UIViewController
    ) -> UIViewController? {
        // Your lookup: resolve video.videoID on your video platform.
        guard let url = streamURL(for: video) else {
            return nil
        }
        let playerVC = AVPlayerViewController()
        playerVC.player = AVPlayer(url: url)
        return playerVC
    }
}
```

> Note: Both methods provide default implementations that return `nil`.
> Override only the methods you need.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Media-and-Links>

## Topics

### Playing Videos

[`videoViewController(for:presentingFrom:)`](/documentation/PSReader/MediaDelegate/videoViewController(for:presentingFrom:))

Provides a view controller for video playback, which the SDK embeds into its
reader media gallery UI.

### Customizing Hotspot Overlays

[`pdfMediaOverlay(for:in:superview:)`](/documentation/PSReader/MediaDelegate/pdfMediaOverlay(for:in:superview:))

Provides a custom media overlay for an embedded media object within a PDF page.

