<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/resolveURL(resource:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC10resolveURL8resource10Foundation0F0VSgSS_tF"
  },
  "title" : "resolveURL(resource:)"
}
-->

# resolveURL(resource:)

Returns a URL for the resource.

```
func resolveURL(resource: String) -> URL?
```

## Parameters

`resource`

The resource reference, as it appears in the
edition’s content.

## Return Value

The URL itself for an absolute `http` reference, the local
file when it’s stored in the edition’s folder, otherwise the legacy
backend URL of that page file, or `nil` when the edition has no
such file.