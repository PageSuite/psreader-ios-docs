<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaObject/background",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaObject(py)background"
  },
  "title" : "background"
}
-->

# background

Whether the hotspot has a background fill.

```
@objc var background: Bool
```

## Discussion

When it’s `true`, [`PSEMediaOverlay`](/documentation/PSReader/PSEMediaOverlay) fills its view with
[`backgroundColor`](/documentation/PSReader/PSEMediaObject/backgroundColor) at [`backgroundAlpha`](/documentation/PSReader/PSEMediaObject/backgroundAlpha).