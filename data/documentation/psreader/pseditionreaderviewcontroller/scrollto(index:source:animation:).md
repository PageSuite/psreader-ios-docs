<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/scrollTo(index:source:animation:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC8scrollTo5index6source9animationySi_ypSgAA0B15ScrollAnimationOtF"
  },
  "title" : "scrollTo(index:source:animation:)"
}
-->

# scrollTo(index:source:animation:)

Scrolls to the spread at `index` (a spread index in the active
paging mode). The `source` token is echoed to [`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol),
and `animation` sets whether the move animates.

```
@MainActor func scrollTo(index: Int, source: Any? = nil, animation: PSEditionScrollAnimation = .automatic)
```