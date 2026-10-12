<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEVideo/videoID",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEVideo(py)videoID"
  },
  "title" : "videoID"
}
-->

# videoID

The video’s identifier on its video platform.

```
@objc var videoID: String?
```

## Discussion

The SDK doesn’t play video itself. Use this identifier with
[`videoAccountID`](/documentation/PSReader/PSEVideo/videoAccountID) and [`videoAccountPolicy`](/documentation/PSReader/PSEVideo/videoAccountPolicy) to load the video from
its platform. The prebuilt reader hands the video to its
[`MediaDelegate`](/documentation/PSReader/MediaDelegate); in a reader you host yourself, the reader’s
[`PSEditionReaderViewController.MediaDelegate`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol) reports
the tap, and the video reaches your own gallery as a
[`PSEMedia.video(_:)`](/documentation/PSReader/PSEMedia/video(_:)) item.