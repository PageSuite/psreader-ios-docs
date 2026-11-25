<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/scrollTo(page:source:animation:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC8scrollTo4page6source9animationyAA7PSEPageC_ypSgAA0B15ScrollAnimationOtF"
  },
  "title" : "scrollTo(page:source:animation:)"
}
-->

# scrollTo(page:source:animation:)

Scrolls to the spread containing `page`. No-op if the page isn’t in
the edition.

```
@MainActor func scrollTo(page: PSEPage, source: Any? = nil, animation: PSEditionScrollAnimation = .automatic)
```