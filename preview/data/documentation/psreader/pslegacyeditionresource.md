<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyEditionResource",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23PSLegacyEditionResourceV"
  },
  "title" : "PSLegacyEditionResource"
}
-->

# PSLegacyEditionResource

A file placed into the edition folder next to the page assets — stylesheets and
fonts the article HTML references by relative name.

```
struct PSLegacyEditionResource
```

## Topics

### Creating a Resource

[`init(name:data:)`](/documentation/PSReader/PSLegacyEditionResource/init(name:data:))

Creates a resource.

### Contents

[`name`](/documentation/PSReader/PSLegacyEditionResource/name)

The file name, relative to the edition folder, that the article HTML
references. Resources with an empty name are skipped.

[`data`](/documentation/PSReader/PSLegacyEditionResource/data)

The file’s contents.

