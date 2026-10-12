<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaLinkOverlay",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaLinkOverlay"
  },
  "title" : "PSEMediaLinkOverlay"
}
-->

# PSEMediaLinkOverlay

The standard overlay for `link`-type hotspots: a tap follows the
hotspot’s `target`.

```
@MainActor class PSEMediaLinkOverlay
```

## Overview

In-edition page links jump the reader. Web links post
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification) for your app to
present, and other schemes (`mailto:`, `tel:`, `sms:`) open through the
system.

## Topics

### Creating the Overlay

[`init(page:linkObject:superview:)`](/documentation/PSReader/PSEMediaLinkOverlay/init(page:linkObject:superview:))

Creates a link overlay that responds to taps.

### Handling Taps

[`tapped(_:)`](/documentation/PSReader/PSEMediaLinkOverlay/tapped(_:))

Follows the hotspot’s `target`.

