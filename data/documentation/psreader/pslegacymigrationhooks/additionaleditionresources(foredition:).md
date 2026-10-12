<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigrationHooks/additionalEditionResources(forEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyMigrationHooksP26additionalEditionResources03forF0SayAA0bF8ResourceVGAA0bF7SummaryV_tF"
  },
  "title" : "additionalEditionResources(forEdition:)"
}
-->

# additionalEditionResources(forEdition:)

Returns extra files, such as stylesheets and fonts, to write into a
migrated edition’s folder for its article HTML to reference.

```
func additionalEditionResources(forEdition edition: PSLegacyEditionSummary) -> [PSLegacyEditionResource]
```

## Parameters

`edition`

The legacy edition being opened.

## Return Value

The files to write.

## Discussion

Called each time a migrated edition opens through
[`open(published:hooks:onProgress:completion:)`](/documentation/PSReader/PSLegacyBridgedEdition/open(published:hooks:onProgress:completion:)).