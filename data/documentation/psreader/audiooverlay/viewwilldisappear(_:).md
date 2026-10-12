<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioOverlay/viewWillDisappear(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)AudioOverlay(im)viewWillDisappear:"
  },
  "title" : "viewWillDisappear(_:)"
}
-->

# viewWillDisappear(_:)

Removes the highlight from the reader’s navigation bar button for the
overlay when the reader dismisses the overlay from a popover.

```
@MainActor override func viewWillDisappear(_ animated: Bool)
```

## Parameters

`animated`

If `true`, the disappearance is animated.

## Discussion

The change animates alongside the dismissal. Subclasses that override
this method must call `super`.