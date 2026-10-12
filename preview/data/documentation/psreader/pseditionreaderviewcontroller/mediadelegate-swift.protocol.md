<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC13MediaDelegateP"
  },
  "title" : "PSEditionReaderViewController.MediaDelegate"
}
-->

# PSEditionReaderViewController.MediaDelegate

Handles media hotspots and embeds on the reader’s pages.

```
protocol MediaDelegate : AnyObject
```

## Overview

All methods have default implementations: the default overlay factory
serves the standard link and article overlays, taps are ignored, and
page URLs come from the page itself.

To handle media and link taps in your own reader screen, see
[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps).

## Topics

### Handling Taps

[`didTapMediaObject(_:in:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapMediaObject(_:in:))

Called when the user taps a media hotspot on a page.

[`didTapMedia(atIndex:in:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapMedia(atIndex:in:))

Called when the user taps an item in a page’s media list.

[`didTapReplacedEmbed(atIndex:originalHTML:type:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapReplacedEmbed(atIndex:originalHTML:type:))

Called when the user taps the placeholder that stands in for a
third-party embed (the SDK replaces embeds until tapped).

### Choosing Overlays

[`mediaOverlay(for:in:superview:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/mediaOverlay(for:in:superview:))

Returns the overlay view to place over a media hotspot, or `nil`
for no overlay. The default dispatches on `mediaObject.type` via
`defaultMediaOverlay(for:in:superview:)`.

[`defaultMediaOverlay(for:in:superview:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/defaultMediaOverlay(for:in:superview:))

Returns the reader’s standard overlay for a hotspot.

### Templated Page Resources

[`baseURL(for:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/baseURL(for:))

The base URL a page’s HTML resolves relative references against.
The default returns the page’s own `baseURL`.

[`editionLogoURL(for:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/editionLogoURL(for:))

A logo image URL for templated pages, or `nil` for none (the
default).

