<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/MediaDelegate/videoViewController(for:presentingFrom:)-5708i",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13MediaDelegatePAAE19videoViewController3for14presentingFromSo06UIViewF0CSgAA8PSEVideoC_AHtF"
  },
  "title" : "videoViewController(for:presentingFrom:)"
}
-->

# videoViewController(for:presentingFrom:)

Returns `nil`, so videos in the media gallery don’t play.

```
@MainActor func videoViewController(for video: PSEVideo, presentingFrom: UIViewController) -> UIViewController?
```

## Parameters

`video`

The video to play.

`presentingFrom`

The view controller in which the video playback
controller would be embedded.

## Return Value

`nil`.