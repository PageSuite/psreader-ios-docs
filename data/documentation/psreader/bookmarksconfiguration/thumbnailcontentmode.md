<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/BookmarksConfiguration/thumbnailContentMode",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22BookmarksConfigurationV20thumbnailContentModeAA05ImageeF0Ovp"
  },
  "title" : "thumbnailContentMode"
}
-->

# thumbnailContentMode

Content mode determining how bookmark thumbnails scale and fit within their containers.

```
var thumbnailContentMode: ImageContentMode
```

## Discussion

Default is `.fitToWidth`, scaling thumbnails to fill their width proportionally.
This may result in vertically cropped thumbnails. If that is not desired change to `.fitToHeight`.

Note: `flexibleHeight` layouts are not supported in the bookmarks view.