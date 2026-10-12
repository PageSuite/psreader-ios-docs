<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioBannerViewController/isFloating",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25AudioBannerViewControllerP10isFloatingSbvp"
  },
  "title" : "isFloating"
}
-->

# isFloating

Controls how the banner is positioned relative to the reader content.

```
@MainActor var isFloating: Bool { get }
```

## Discussion

The reader lays the banner out one of two ways:

- When `true`, the banner floats above content (SDK applies bottom insets).
- When `false`, the banner is stacked below content (no additional insets).