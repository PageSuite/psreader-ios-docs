<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEVideo",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEVideo"
  },
  "title" : "PSEVideo"
}
-->

# PSEVideo

A video embedded in an article.

```
@objc class PSEVideo
```

## Topics

### Identity

[`videoID`](/documentation/PSReader/PSEVideo/videoID)

The video’s identifier on its video platform.

[`videoAccountID`](/documentation/PSReader/PSEVideo/videoAccountID)

The video platform account that hosts the video, as sent by the
backend.

[`videoAccountPolicy`](/documentation/PSReader/PSEVideo/videoAccountPolicy)

The video platform account’s policy value, as sent by the backend.

### Display

[`videoCaption`](/documentation/PSReader/PSEVideo/videoCaption)

The video’s caption.

[`isLeadAsset`](/documentation/PSReader/PSEVideo/isLeadAsset)

Whether the video is its article’s lead asset.

### Poster Image

[`videoImageURLs`](/documentation/PSReader/PSEVideo/videoImageURLs)

Where to load the video’s poster image from, in order of preference:
the main image, then a smaller rendition when there is one.

[`videoImageOriginalURL`](/documentation/PSReader/PSEVideo/videoImageOriginalURL)

The poster image’s original URL, when the backend sends one.

[`crops`](/documentation/PSReader/PSEVideo/crops)

Fixed aspect-ratio crops of the poster image, when the backend
supplies them.

