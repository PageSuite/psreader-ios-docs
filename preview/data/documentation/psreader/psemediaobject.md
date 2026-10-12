<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaObject",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaObject"
  },
  "title" : "PSEMediaObject"
}
-->

# PSEMediaObject

An interactive hotspot on a page: a tappable region that links out,
jumps within the edition, or plays media.

```
@objc class PSEMediaObject
```

## Overview

[`type`](/documentation/PSReader/PSEMediaObject/type) discriminates the behavior (`link`, `article`, video kinds, …);
the geometry fields position the hotspot on the page. The reader covers
hotspots with [`PSEMediaOverlay`](/documentation/PSReader/PSEMediaOverlay) views chosen by the
[`PSEditionReaderViewController.MediaDelegate`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol).

## Topics

### Identity

[`mediaObjectGUID`](/documentation/PSReader/PSEMediaObject/mediaObjectGUID)

The hotspot’s unique identifier.

[`type`](/documentation/PSReader/PSEMediaObject/type)

The kind of hotspot, such as `link`, `article`, or `video`.

[`name`](/documentation/PSReader/PSEMediaObject/name)

The hotspot’s name, as sent by the backend.

[`title`](/documentation/PSReader/PSEMediaObject/title)

The hotspot’s title, as sent by the backend.

[`editionGUID`](/documentation/PSReader/PSEMediaObject/editionGUID)

The GUID of the edition the hotspot belongs to.

[`editionPageGUID`](/documentation/PSReader/PSEMediaObject/editionPageGUID)

The hotspot’s edition page GUID, as sent by the backend.

### Position on the Page

[`x`](/documentation/PSReader/PSEMediaObject/x)

The hotspot’s left edge, as a percentage of the page’s width (0–100).

[`y`](/documentation/PSReader/PSEMediaObject/y)

The hotspot’s top edge, as a percentage of the page’s height from the
top (0–100).

[`width`](/documentation/PSReader/PSEMediaObject/width)

The hotspot’s width, as a percentage of the page’s width.

[`height`](/documentation/PSReader/PSEMediaObject/height)

The hotspot’s height, as a percentage of the page’s height.

### Tap Target

[`target`](/documentation/PSReader/PSEMediaObject/target)

Where a tap on the hotspot leads, such as a URL.

[`isURL`](/documentation/PSReader/PSEMediaObject/isURL)

Whether the backend flags the hotspot’s [`target`](/documentation/PSReader/PSEMediaObject/target) as a web URL.

[`isEmail`](/documentation/PSReader/PSEMediaObject/isEmail)

Whether the backend flags the hotspot’s [`target`](/documentation/PSReader/PSEMediaObject/target) as an email
address.

[`isPage`](/documentation/PSReader/PSEMediaObject/isPage)

Whether the backend flags the hotspot’s [`target`](/documentation/PSReader/PSEMediaObject/target) as a page in the
edition.

[`feedPageGUID`](/documentation/PSReader/PSEMediaObject/feedPageGUID)

For `article` hotspots, the [`pageguid`](/documentation/PSReader/PSEPage/pageguid) of the article page
a tap jumps to.

### Media

[`images`](/documentation/PSReader/PSEMediaObject/images)

The images attached to the hotspot, such as a gallery’s pictures, or
`nil` when it has none.

[`brightcoveID`](/documentation/PSReader/PSEMediaObject/brightcoveID)

The Brightcove video ID for a video hotspot, or `nil` when it has
none.

[`isVerticalVideo`](/documentation/PSReader/PSEMediaObject/isVerticalVideo)

Whether [`brightcoveID`](/documentation/PSReader/PSEMediaObject/brightcoveID) identifies a vertical video.

### Appearance

[`background`](/documentation/PSReader/PSEMediaObject/background)

Whether the hotspot has a background fill.

[`backgroundColor`](/documentation/PSReader/PSEMediaObject/backgroundColor)

The background fill color, as a hex string.

[`backgroundAlpha`](/documentation/PSReader/PSEMediaObject/backgroundAlpha)

The opacity of the background fill, from 0 to 1.

[`backgroundImage`](/documentation/PSReader/PSEMediaObject/backgroundImage)

The hotspot’s background image, as sent by the backend.

[`border`](/documentation/PSReader/PSEMediaObject/border)

Whether the hotspot has a border.

[`borderColor`](/documentation/PSReader/PSEMediaObject/borderColor)

The border color, as a hex string.

[`borderAlpha`](/documentation/PSReader/PSEMediaObject/borderAlpha)

The opacity of the border, from 0 to 1.

