<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveConfiguration/thumbnailContentMode",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ArchiveConfigurationV20thumbnailContentModeAA05ImageeF0Ovp"
  },
  "title" : "thumbnailContentMode"
}
-->

# thumbnailContentMode

Content mode for standard archive thumbnails.

```
var thumbnailContentMode: ImageContentMode
```

## Discussion

Applies to regular archive cells. The latest edition hero cell uses
[`latestPaperThumbnailContentMode`](/documentation/PSReader/ArchiveConfiguration/latestPaperThumbnailContentMode) when set, otherwise derives its
mode from this property.

Defaults to [`ImageContentMode.fitToWidth`](/documentation/PSReader/ImageContentMode/fitToWidth), which scales the thumbnail
to the available width and may crop vertically.