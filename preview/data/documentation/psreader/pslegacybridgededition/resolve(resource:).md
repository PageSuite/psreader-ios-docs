<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/resolve(resource:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC7resolve8resourceSSSgSS_tF"
  },
  "title" : "resolve(resource:)"
}
-->

# resolve(resource:)

Returns a location for the resource.

```
func resolve(resource: String) -> String?
```

## Parameters

`resource`

The resource reference, as it appears in the
edition’s content.

## Return Value

The reference itself when it’s an absolute `http` URL or a
file stored in the edition’s folder, otherwise the legacy backend
URL of that page file, or `nil` when the edition has no such file.