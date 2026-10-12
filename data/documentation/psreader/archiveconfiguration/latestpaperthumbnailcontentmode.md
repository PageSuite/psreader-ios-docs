<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveConfiguration/latestPaperThumbnailContentMode",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ArchiveConfigurationV31latestPaperThumbnailContentModeAA05ImagegH0OSgvp"
  },
  "title" : "latestPaperThumbnailContentMode"
}
-->

# latestPaperThumbnailContentMode

Optional content mode override for the latest edition hero cell.

```
var latestPaperThumbnailContentMode: ImageContentMode?
```

## Discussion

The hero cell spans the full archive width, so it often needs a
different layout strategy than regular cells. In particular,
[`ImageContentMode.flexibleHeight(estimatedAspectRatio:)`](/documentation/PSReader/ImageContentMode/flexibleHeight(estimatedAspectRatio:)) can cause
the hero to grow taller than the archive container when maintaining
the aspect ratio at that width.

You usually do not need to set this. When `nil`, the SDK derives a
mode from [`thumbnailContentMode`](/documentation/PSReader/ArchiveConfiguration/thumbnailContentMode): [`ImageContentMode.fitToWidth`](/documentation/PSReader/ImageContentMode/fitToWidth)
and [`ImageContentMode.fitToHeight`](/documentation/PSReader/ImageContentMode/fitToHeight) are used as-is, but
[`ImageContentMode.flexibleHeight(estimatedAspectRatio:)`](/documentation/PSReader/ImageContentMode/flexibleHeight(estimatedAspectRatio:)) is replaced
with [`ImageContentMode.fitToHeight`](/documentation/PSReader/ImageContentMode/fitToHeight), which caps the hero’s height
within the container while still showing the full image uncropped.