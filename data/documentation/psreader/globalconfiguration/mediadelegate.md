<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration/mediaDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV13mediaDelegateAA05MediaE0_pSgvp"
  },
  "title" : "mediaDelegate"
}
-->

# mediaDelegate

Optional delegate for enabling video and media playback. No playback functionality is provided by default.

```
var mediaDelegate: MediaDelegate?
```

## Discussion

The SDK has no video player of its own: without this delegate, videos
in the reader’s media gallery can’t play.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Media-and-Links#Playing-Videos>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/MediaDelegate``