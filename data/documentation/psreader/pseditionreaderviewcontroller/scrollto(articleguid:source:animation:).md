<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/scrollTo(articleGUID:source:animation:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC8scrollTo11articleGUID6source9animationySS_ypSgAA0B15ScrollAnimationOtF"
  },
  "title" : "scrollTo(articleGUID:source:animation:)"
}
-->

# scrollTo(articleGUID:source:animation:)

Scrolls to the spread presenting the article with `articleGUID`.
No-op if no article matches.

```
@MainActor func scrollTo(articleGUID: String, source: Any? = nil, animation: PSEditionScrollAnimation = .automatic)
```