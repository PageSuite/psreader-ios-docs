<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/scrollTo(article:source:animation:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC8scrollTo7article6source9animationyAA10PSEArticleC_ypSgAA0B15ScrollAnimationOtF"
  },
  "title" : "scrollTo(article:source:animation:)"
}
-->

# scrollTo(article:source:animation:)

Scrolls to the spread presenting `article`. No-op if the article
isn’t in the edition.

```
@MainActor func scrollTo(article: PSEArticle, source: Any? = nil, animation: PSEditionScrollAnimation = .automatic)
```