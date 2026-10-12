<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyArticleContext/fetchData(forLegacyURL:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyArticleContextV9fetchData12forLegacyURL10Foundation0F0VSgSS_tYaF"
  },
  "title" : "fetchData(forLegacyURL:)"
}
-->

# fetchData(forLegacyURL:)

Bytes for the given absolute legacy URL: disk (sha1+md5) first, then network.

```
func fetchData(forLegacyURL url: String) async -> Data?
```