<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ImageContentMode",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16ImageContentModeO"
  },
  "title" : "ImageContentMode"
}
-->

# ImageContentMode

Defines how an image should be resized and positioned within its container.

```
enum ImageContentMode
```

## Topics

### Content Modes

[`ImageContentMode.fitToWidth`](/documentation/PSReader/ImageContentMode/fitToWidth)

The image is scaled proportionally to fit the width of its container,
potentially cropping vertically.

[`ImageContentMode.fitToHeight`](/documentation/PSReader/ImageContentMode/fitToHeight)

The image is scaled proportionally to fit the height of its container,
potentially cropping horizontally.

[`ImageContentMode.flexibleHeight(estimatedAspectRatio:)`](/documentation/PSReader/ImageContentMode/flexibleHeight(estimatedAspectRatio:))

The image is scaled proportionally to fit the width of its container,
while the height adjusts dynamically maintaining the images aspect ratio.

