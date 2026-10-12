<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/dataTask(for:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC8dataTask3for10completionAA07PSEDataF0_pSgSS_y10Foundation4DataVSgctF"
  },
  "title" : "dataTask(for:completion:)"
}
-->

# dataTask(for:completion:)

Creates an HTTP fetch for the resource: an absolute `http` reference
as it is, or a page file from the legacy backend.

```
func dataTask(for resource: String, completion: @escaping (Data?) -> Void) -> PSEDataTask?
```

## Parameters

`resource`

The resource reference, as it appears in the edition’s
content.

`completion`

Called with the fetched data, or `nil` when the fetch
fails.

## Return Value

The fetch’s task, or `nil` when the resource is neither an
absolute `http` URL nor a page file of this edition.