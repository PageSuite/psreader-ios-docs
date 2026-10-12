<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaArticleOverlay/tapped(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaArticleOverlay(im)tapped:"
  },
  "title" : "tapped(_:)"
}
-->

# tapped(_:)

Jumps the reader to the page named by the hotspot’s `feedPageGUID`.

```
@objc @MainActor func tapped(_ sender: Any?)
```

## Parameters

`sender`

The object that triggered the tap; unused.

## Discussion

The jump reaches your
[`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) with a
[`PageJumpNavigationSource`](/documentation/PSReader/PageJumpNavigationSource) carrying this overlay’s page and hotspot.
Does nothing when the hotspot has no `feedPageGUID`.