<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/pagesInImage",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)pagesInImage"
  },
  "title" : "pagesInImage"
}
-->

# pagesInImage

The number of images [`highRes`](/documentation/PSReader/PSEPage/highRes) spans; `1` by default.

```
@objc var pagesInImage: Int
```

## Discussion

When it’s greater than `1`, the extra images share the [`highRes`](/documentation/PSReader/PSEPage/highRes)
URL with `_2`, `_3`, and so on inserted before the file extension.