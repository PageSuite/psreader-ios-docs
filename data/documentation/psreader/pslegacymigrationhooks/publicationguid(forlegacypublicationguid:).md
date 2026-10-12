<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyMigrationHooks/publicationGUID(forLegacyPublicationGUID:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyMigrationHooksP15publicationGUID020forLegacyPublicationF0S2S_tF"
  },
  "title" : "publicationGUID(forLegacyPublicationGUID:)"
}
-->

# publicationGUID(forLegacyPublicationGUID:)

Returns the value to record as a migrated catalog entry’s
`publicationGUID`, given the legacy edition’s replica publication
GUID.

```
func publicationGUID(forLegacyPublicationGUID guid: String) -> String
```

## Parameters

`guid`

The legacy edition’s replica publication GUID.

## Return Value

The value to record.