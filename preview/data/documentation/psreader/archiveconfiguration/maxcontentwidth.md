<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveConfiguration/maxContentWidth",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ArchiveConfigurationV15maxContentWidth14CoreFoundation7CGFloatVSgvp"
  },
  "title" : "maxContentWidth"
}
-->

# maxContentWidth

Maximum width of the archive content in regular width environments.

```
var maxContentWidth: CGFloat?
```

## Discussion

Content wider than this is centered, with the archive itself still filling
the screen. Defaults to `nil`, which lets the content fill the available width.

> Note: Compact width environments ignore this value.