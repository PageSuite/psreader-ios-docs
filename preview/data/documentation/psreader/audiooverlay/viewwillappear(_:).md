<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioOverlay/viewWillAppear(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)AudioOverlay(im)viewWillAppear:"
  },
  "title" : "viewWillAppear(_:)"
}
-->

# viewWillAppear(_:)

Highlights the reader’s navigation bar button for the overlay when the
reader presents the overlay as a popover.

```
@MainActor override func viewWillAppear(_ animated: Bool)
```

## Parameters

`animated`

If `true`, the appearance is animated.

## Discussion

The highlight animates alongside the presentation. Subclasses that
override this method must call `super`.