<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyArticleContext/localImageReference(forLegacyURL:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyArticleContextV19localImageReference12forLegacyURLS2S_tF"
  },
  "title" : "localImageReference(forLegacyURL:)"
}
-->

# localImageReference(forLegacyURL:)

The edition-folder-relative filename the given legacy image URL takes once
materialized. Include the URL in `imageURLsToMaterialize` for the file to exist.

```
func localImageReference(forLegacyURL url: String) -> String
```