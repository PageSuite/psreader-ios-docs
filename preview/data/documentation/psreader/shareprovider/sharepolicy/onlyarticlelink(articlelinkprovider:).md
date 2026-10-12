<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareProvider/SharePolicy/onlyArticleLink(articleLinkProvider:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareProviderC0B6PolicyO15onlyArticleLinkyAeA0fgbC0C_tcAEmF"
  },
  "title" : "ShareProvider.SharePolicy.onlyArticleLink(articleLinkProvider:)"
}
-->

# ShareProvider.SharePolicy.onlyArticleLink(articleLinkProvider:)

Shares only direct article links to content on the publisher’s website.

```
case onlyArticleLink(articleLinkProvider: ArticleLinkShareProvider = .init())
```

## Parameters

`articleLinkProvider`

Provider for article links hosted externally.
Defaults to a new instance of `ArticleLinkShareProvider`.