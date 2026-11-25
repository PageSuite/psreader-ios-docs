<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/isSupportedPage(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Type Method",
  "symbol" : {
    "kind" : "Type Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10PSEEditionC15isSupportedPageySbAA7PSEPageCFZ"
  },
  "title" : "isSupportedPage(_:)"
}
-->

# isSupportedPage(_:)

Whether the SDK understands a page’s type well enough to show it.
Pages without a type pass; the type is optional in older feeds.
Third-party advert pages pass regardless of provider: whether one
can actually be rendered is decided by the filter the reader applies
through [`applyPageFilter(_:)`](/documentation/PSReader/PSEEdition/applyPageFilter(_:)) when it opens the edition.

```
static func isSupportedPage(_ page: PSEPage) -> Bool
```