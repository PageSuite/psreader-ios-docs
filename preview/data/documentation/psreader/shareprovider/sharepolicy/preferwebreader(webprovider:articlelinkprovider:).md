<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareProvider/SharePolicy/preferWebReader(webProvider:articleLinkProvider:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareProviderC0B6PolicyO15preferWebReaderyAeA0fgbC0C_AA011ArticleLinkbC0CtcAEmF"
  },
  "title" : "ShareProvider.SharePolicy.preferWebReader(webProvider:articleLinkProvider:)"
}
-->

# ShareProvider.SharePolicy.preferWebReader(webProvider:articleLinkProvider:)

Prefers sharing links to the web reader but falls back to direct
article links if web reader links are unavailable.

```
case preferWebReader(webProvider: WebReaderShareProvider, articleLinkProvider: ArticleLinkShareProvider = .init())
```

## Parameters

`webProvider`

A configured `WebReaderShareProvider` responsible
for generating share links to your web reader.

`articleLinkProvider`

Provider for article links hosted externally.
Defaults to a new instance of `ArticleLinkShareProvider`.