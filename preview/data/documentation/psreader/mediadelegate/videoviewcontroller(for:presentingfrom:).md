<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/MediaDelegate/videoViewController(for:presentingFrom:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13MediaDelegateP19videoViewController3for14presentingFromSo06UIViewF0CSgAA8PSEVideoC_AHtF"
  },
  "title" : "videoViewController(for:presentingFrom:)"
}
-->

# videoViewController(for:presentingFrom:)

Provides a view controller for video playback, which the SDK embeds into its
reader media gallery UI.

```
@MainActor func videoViewController(for video: PSEVideo, presentingFrom: UIViewController) -> UIViewController?
```

## Parameters

`video`

A `PSEVideo` object containing information required for playback.

`presentingFrom`

The view controller in which the video playback controller is embedded.

## Return Value

A view controller responsible for video playback, or `nil` if the video should not be played.

## Discussion

The SDK doesn’t play video itself. Implement this method to play
videos in the built-in media gallery.