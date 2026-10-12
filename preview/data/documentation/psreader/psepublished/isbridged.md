<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/isBridged",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished(py)isBridged"
  },
  "title" : "isBridged"
}
-->

# isBridged

Whether this edition is a download migrated from the legacy SDK.

```
@objc var isBridged: Bool
```

## Discussion

Open a migrated edition with [`PSLegacyBridgedEdition`](/documentation/PSReader/PSLegacyBridgedEdition); see
[Adding a Download Button](/documentation/PSReader/Adding-a-Download-Button). Editions from the catalog are never
migrated, so this is `false` for them.