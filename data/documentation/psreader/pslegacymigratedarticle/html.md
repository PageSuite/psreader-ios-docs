<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigratedArticle/html",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PSLegacyMigratedArticleV4htmlSSvp"
  },
  "title" : "html"
}
-->

# html

Render-ready page HTML, loaded verbatim from a file inside the edition
folder — no SDK template processing touches it. Reference materialized
images and edition resources by their edition-folder-relative names (see
`PSLegacyArticleContext.localImageReference(forLegacyURL:)`); absolute
http(s) URLs are also allowed but load online only.

```
var html: String
```