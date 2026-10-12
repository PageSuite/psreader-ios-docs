<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/cachedData(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC10cachedData3for10Foundation0F0VSgSS_tF"
  },
  "title" : "cachedData(for:)"
}
-->

# cachedData(for:)

Returns the resource’s bytes if it’s stored in the edition’s folder.

```
func cachedData(for resource: String) -> Data?
```

## Parameters

`resource`

The resource reference, as it appears in the
edition’s content.

## Return Value

The stored data, or `nil` when the edition’s folder doesn’t
hold the resource yet.