<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaObject/brightcoveID",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaObject(py)brightcoveID"
  },
  "title" : "brightcoveID"
}
-->

# brightcoveID

The Brightcove video ID for a video hotspot, or `nil` when it has
none.

```
@objc var brightcoveID: String?
```

## Discussion

On iPhone the ID of the vertical version is used when the payload
provides one; see [`isVerticalVideo`](/documentation/PSReader/PSEMediaObject/isVerticalVideo).