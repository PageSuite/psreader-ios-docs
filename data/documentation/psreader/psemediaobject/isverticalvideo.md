<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaObject/isVerticalVideo",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaObject(py)isVerticalVideo"
  },
  "title" : "isVerticalVideo"
}
-->

# isVerticalVideo

Whether [`brightcoveID`](/documentation/PSReader/PSEMediaObject/brightcoveID) identifies a vertical video.

```
@objc var isVerticalVideo: Bool
```

## Discussion

It’s only ever `true` on iPhone, which prefers a video’s vertical
version when one exists.