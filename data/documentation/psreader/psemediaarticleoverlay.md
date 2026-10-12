<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaArticleOverlay",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaArticleOverlay"
  },
  "title" : "PSEMediaArticleOverlay"
}
-->

# PSEMediaArticleOverlay

The standard overlay for `article`-type hotspots: a tap jumps the reader
to the linked article’s page.

```
@MainActor class PSEMediaArticleOverlay
```

## Topics

### Creating the Overlay

[`init(page:articleObject:superview:)`](/documentation/PSReader/PSEMediaArticleOverlay/init(page:articleObject:superview:))

Creates an article overlay that responds to taps.

### Handling Taps

[`tapped(_:)`](/documentation/PSReader/PSEMediaArticleOverlay/tapped(_:))

Jumps the reader to the page named by the hotspot’s `feedPageGUID`.

