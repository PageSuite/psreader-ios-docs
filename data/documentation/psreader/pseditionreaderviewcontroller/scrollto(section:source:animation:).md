<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/scrollTo(section:source:animation:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC8scrollTo7section6source9animationyAA10PSESectionC_ypSgAA0B15ScrollAnimationOtF"
  },
  "title" : "scrollTo(section:source:animation:)"
}
-->

# scrollTo(section:source:animation:)

Scrolls to the first article spread of `section`. No-op if the
section isn’t in the edition.

```
@MainActor func scrollTo(section: PSESection, source: Any? = nil, animation: PSEditionScrollAnimation = .automatic)
```