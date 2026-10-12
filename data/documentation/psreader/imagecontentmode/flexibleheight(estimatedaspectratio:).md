<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ImageContentMode/flexibleHeight(estimatedAspectRatio:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16ImageContentModeO14flexibleHeightyAC14CoreFoundation7CGFloatV_tcACmF"
  },
  "title" : "ImageContentMode.flexibleHeight(estimatedAspectRatio:)"
}
-->

# ImageContentMode.flexibleHeight(estimatedAspectRatio:)

The image is scaled proportionally to fit the width of its container,
while the height adjusts dynamically maintaining the images aspect ratio.

```
case flexibleHeight(estimatedAspectRatio: CGFloat)
```

## Discussion

An `estimatedAspectRatio` is used as a placeholder while the image is
loading and its true aspect ratio is not yet known. This estimate helps
maintain stable layout during loading and is refined automatically at
runtime as the system learns the typical aspect ratios for a given
publication. Once the actual image is available, the layout is updated
if the true aspect ratio differs from the estimate.