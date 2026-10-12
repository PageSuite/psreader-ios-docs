<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareProvider/SharePolicy/preferArticleLink(webProvider:articleLinkProvider:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareProviderC0B6PolicyO17preferArticleLinkyAeA09WebReaderbC0C_AA0fgbC0CtcAEmF"
  },
  "title" : "ShareProvider.SharePolicy.preferArticleLink(webProvider:articleLinkProvider:)"
}
-->

# ShareProvider.SharePolicy.preferArticleLink(webProvider:articleLinkProvider:)

Prefers sharing direct links to articles on the publisher’s website but
falls back to the web reader when article links are unavailable.

```
case preferArticleLink(webProvider: WebReaderShareProvider, articleLinkProvider: ArticleLinkShareProvider = .init())
```

## Parameters

`webProvider`

A configured `WebReaderShareProvider` responsible
for generating share links to your web reader.

`articleLinkProvider`

Provider for article links hosted externally.
Defaults to a new instance of `ArticleLinkShareProvider`.