<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMediaLinkOverlay/tapped(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMediaLinkOverlay(im)tapped:"
  },
  "title" : "tapped(_:)"
}
-->

# tapped(_:)

Follows the hotspot’s `target`.

```
@objc @MainActor func tapped(_ sender: Any?)
```

## Parameters

`sender`

The object that triggered the tap; unused.

## Discussion

A `pagejump://` target followed by a page GUID jumps the reader to
that page, reaching your
[`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) with a
[`PageJumpNavigationSource`](/documentation/PSReader/PageJumpNavigationSource). Any other target is treated as a URL,
with `https://` assumed when it has no scheme: `http` and `https`
URLs post [`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification),
and other schemes open through the system. Does nothing when the
hotspot has no `target`.