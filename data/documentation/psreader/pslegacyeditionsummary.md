<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyEditionSummary",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyEditionSummaryV"
  },
  "title" : "PSLegacyEditionSummary"
}
-->

# PSLegacyEditionSummary

Read-only view of a legacy edition handed to hooks.

```
struct PSLegacyEditionSummary
```

## Topics

### Identity

[`editionGUID`](/documentation/PSReader/PSLegacyEditionSummary/editionGUID)

The legacy edition’s GUID, which the migrated catalog entry keeps as
its edition GUID.

[`publicationGUID`](/documentation/PSReader/PSLegacyEditionSummary/publicationGUID)

The replica publication GUID of the legacy edition’s publication.

### Display

[`name`](/documentation/PSReader/PSLegacyEditionSummary/name)

The legacy edition’s name.

[`publishDate`](/documentation/PSReader/PSLegacyEditionSummary/publishDate)

The legacy edition’s publish date, or `nil` if the legacy SDK didn’t
record one.

### Download State

[`downloadedDate`](/documentation/PSReader/PSLegacyEditionSummary/downloadedDate)

When the legacy SDK downloaded the edition.

[`isEncrypted`](/documentation/PSReader/PSLegacyEditionSummary/isEncrypted)

Whether the legacy replica system flagged the edition as encrypted.

