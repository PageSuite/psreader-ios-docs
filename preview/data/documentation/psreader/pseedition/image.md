<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/image",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEEdition(py)image"
  },
  "title" : "image"
}
-->

# image

URL of the edition’s cover image, when the edition payload includes
one.

```
@objc var image: String?
```

## Discussion

For archive covers, use [`image`](/documentation/PSReader/PSEPublished/image), which is available
before the edition loads.