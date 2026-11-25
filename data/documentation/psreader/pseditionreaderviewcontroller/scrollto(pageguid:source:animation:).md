<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/scrollTo(pageGUID:source:animation:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC8scrollTo8pageGUID6source9animationySS_ypSgAA0B15ScrollAnimationOtF"
  },
  "title" : "scrollTo(pageGUID:source:animation:)"
}
-->

# scrollTo(pageGUID:source:animation:)

Scrolls to the spread containing the page with `pageGUID`. No-op if
no page matches.

```
@MainActor func scrollTo(pageGUID: String, source: Any? = nil, animation: PSEditionScrollAnimation = .automatic)
```