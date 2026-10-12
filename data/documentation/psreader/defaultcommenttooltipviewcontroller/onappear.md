<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentTooltipViewController/onAppear",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader35DefaultCommentTooltipViewControllerC8onAppearyycSgvp"
  },
  "title" : "onAppear"
}
-->

# onAppear

Called when the tooltip appears on screen (`viewDidAppear`).

```
@MainActor var onAppear: (() -> Void)?
```

## Discussion

Use this to track that the tooltip was actually presented, as opposed
to merely created.