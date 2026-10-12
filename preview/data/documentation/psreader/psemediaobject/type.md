<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaObject/type",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaObject(py)type"
  },
  "title" : "type"
}
-->

# type

The kind of hotspot, such as `link`, `article`, or `video`.

```
@objc var type: String?
```

## Discussion

Compare it case-insensitively: payloads may send uppercase values.
The reader’s default overlays handle `link` and `article` hotspots;
edition templates can define other types.