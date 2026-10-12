<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/highRes",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)highRes"
  },
  "title" : "highRes"
}
-->

# highRes

The URL of a high-resolution image of the page, as sent by the
backend.

```
@objc var highRes: String?
```

## Discussion

The prebuilt reader prints templated pages from this image. See
[`pagesInImage`](/documentation/PSReader/PSEPage/pagesInImage) for pages that span several images.