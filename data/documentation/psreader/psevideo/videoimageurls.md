<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEVideo/videoImageURLs",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEVideo(py)videoImageURLs"
  },
  "title" : "videoImageURLs"
}
-->

# videoImageURLs

Where to load the video’s poster image from, in order of preference:
the main image, then a smaller rendition when there is one.

```
@objc var videoImageURLs: [String]
```

## Discussion

Entries can be paths relative to the edition’s content or absolute
URLs. Resolve them through the open edition’s
[`resourceManager`](/documentation/PSReader/PSEEditionSource/resourceManager) and use the first that resolves.