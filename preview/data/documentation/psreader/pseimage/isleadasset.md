<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEImage/isLeadAsset",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEImage(py)isLeadAsset"
  },
  "title" : "isLeadAsset"
}
-->

# isLeadAsset

Whether the image is its article’s lead asset.

```
@objc var isLeadAsset: Bool
```

## Discussion

[`leadAsset()`](/documentation/PSReader/PSEArticle/leadAsset()) picks a flagged lead video first, then a
flagged lead image.