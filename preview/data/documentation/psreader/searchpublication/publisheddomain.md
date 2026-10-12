<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchPublication/publishedDomain",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17SearchPublicationV15publishedDomainSSSgvp"
  },
  "title" : "publishedDomain"
}
-->

# publishedDomain

The base domain used for loading edition content for this publication.

```
let publishedDomain: String?
```

## Discussion

When non-nil, overrides the default published domain
(`"https://published.pagesuite.com/"`) for this publication. This is
needed when a publication’s content is hosted on a custom domain.