<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyEditionSummary/isEncrypted",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyEditionSummaryV11isEncryptedSbvp"
  },
  "title" : "isEncrypted"
}
-->

# isEncrypted

Whether the legacy replica system flagged the edition as encrypted.

```
let isEncrypted: Bool
```

## Discussion

Migration doesn’t act on it; check it in
[`shouldMigrate(edition:)`](/documentation/PSReader/PSLegacyMigrationHooks/shouldMigrate(edition:)) to skip such
editions.