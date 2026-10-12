<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyEditionSummary/downloadedDate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyEditionSummaryV14downloadedDate10Foundation0F0VSgvp"
  },
  "title" : "downloadedDate"
}
-->

# downloadedDate

When the legacy SDK downloaded the edition.

```
let downloadedDate: Date?
```

## Discussion

`nil` when the legacy SDK didn’t record it, and in the summary passed
to the hooks when a migrated edition opens.