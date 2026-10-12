<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:)",
  "metadataVersion" : "0.1.0",
  "role" : "Type Method",
  "symbol" : {
    "kind" : "Type Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC4open9published5hooks10onProgressAcA12PSEPublishedC_AA0B14MigrationHooks_pySfcSgtYaKFZ"
  },
  "title" : "open(published:hooks:onProgress:)"
}
-->

# open(published:hooks:onProgress:)

Opens a bridged legacy download.

```
static func open(published: PSEPublished, hooks: PSLegacyMigrationHooks = PSLegacyDefaultMigrationHooks(), onProgress: ((Float) -> Void)? = nil) async throws -> PSLegacyBridgedEdition
```

## Discussion

See [`open(published:hooks:onProgress:completion:)`](/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:completion:)) for parameter
details.