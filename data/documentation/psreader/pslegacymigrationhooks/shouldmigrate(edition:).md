<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigrationHooks/shouldMigrate(edition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyMigrationHooksP13shouldMigrate7editionSbAA0B14EditionSummaryV_tF"
  },
  "title" : "shouldMigrate(edition:)"
}
-->

# shouldMigrate(edition:)

Returns whether to migrate an edition downloaded with the legacy SDK.

```
func shouldMigrate(edition: PSLegacyEditionSummary) -> Bool
```

## Parameters

`edition`

The legacy edition.

## Return Value

`true` to migrate the edition.

## Discussion

Called for each legacy download during
[`migrateLegacyDownloads(hooks:)`](/documentation/PSReader/PSEDownloadManager/migrateLegacyDownloads(hooks:)). Migration runs
once, so an edition left out isn’t offered again. Saved pages migrate
without asking.