<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyArticleContext/hasCachedData(forLegacyURL:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyArticleContextV13hasCachedData12forLegacyURLSbSS_tF"
  },
  "title" : "hasCachedData(forLegacyURL:)"
}
-->

# hasCachedData(forLegacyURL:)

Returns whether the legacy SDK’s cache holds a copy of the given
absolute legacy URL, without using the network.

```
func hasCachedData(forLegacyURL url: String) -> Bool
```

## Parameters

`url`

The absolute legacy URL to look up.

## Return Value

`true` when a cached copy exists.

## Discussion

The default article template uses it to include only images that are
available offline.