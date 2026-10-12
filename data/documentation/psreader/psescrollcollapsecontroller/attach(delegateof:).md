<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEScrollCollapseController/attach(delegateOf:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27PSEScrollCollapseControllerC6attach10delegateOfySo12UIScrollViewC_tF"
  },
  "title" : "attach(delegateOf:)"
}
-->

# attach(delegateOf:)

Tracks a scroll view by becoming its `delegate`. Use when nothing
else needs the delegate; otherwise use [`attach(panGestureOf:)`](/documentation/PSReader/PSEScrollCollapseController/attach(panGestureOf:)).

```
@MainActor func attach(delegateOf scrollView: UIScrollView)
```