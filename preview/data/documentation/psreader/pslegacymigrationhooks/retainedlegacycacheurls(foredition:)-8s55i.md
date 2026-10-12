<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigrationHooks/retainedLegacyCacheURLs(forEdition:)-8s55i",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyMigrationHooksPAAE23retainedLegacyCacheURLs10forEditionSaySSGSS_tF"
  },
  "title" : "retainedLegacyCacheURLs(forEdition:)"
}
-->

# retainedLegacyCacheURLs(forEdition:)

Returns an empty array, so migration keeps no extra cached files.

```
func retainedLegacyCacheURLs(forEdition editionGUID: String) -> [String]
```

## Parameters

`editionGUID`

The legacy edition’s GUID.

## Return Value

An empty array.