<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEImageCrop/URLs",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEImageCrop(py)URLs"
  },
  "title" : "URLs"
}
-->

# URLs

Where to load the crop from, in order of preference: the main crop,
then a smaller rendition when there is one.

```
@objc var URLs: [String]
```

## Discussion

Entries can be paths relative to the edition’s content or absolute
URLs. Resolve them through the open edition’s
[`resourceManager`](/documentation/PSReader/PSEEditionSource/resourceManager) and use the first that resolves.