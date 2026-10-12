<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEVideo/videoImageOriginalURL",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEVideo(py)videoImageOriginalURL"
  },
  "title" : "videoImageOriginalURL"
}
-->

# videoImageOriginalURL

The poster image’s original URL, when the backend sends one.

```
@objc var videoImageOriginalURL: String?
```

## Discussion

Unlike [`originalURL`](/documentation/PSReader/PSEImage/originalURL), it isn’t included in
[`videoImageURLs`](/documentation/PSReader/PSEVideo/videoImageURLs).