<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaObject/target",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaObject(py)target"
  },
  "title" : "target"
}
-->

# target

Where a tap on the hotspot leads, such as a URL.

```
@objc var target: String?
```

## Discussion

[`PSEMediaLinkOverlay`](/documentation/PSReader/PSEMediaLinkOverlay) follows it: a `pagejump://` target followed by
a page GUID jumps within the edition, and anything else is handled as
a URL.