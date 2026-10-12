<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/resolveURL(resource:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC10resolveURL8resource10Foundation0E0VSgSS_tF"
  },
  "title" : "resolveURL(resource:)"
}
-->

# resolveURL(resource:)

Returns a URL for the resource: the local file once it has
downloaded, otherwise its remote URL.

```
func resolveURL(resource hash: String) -> URL?
```

## Parameters

`hash`

The resource reference, as it appears in the
edition’s content. A reference with a path also matches by its last
component, and absolute `http` URLs are returned as they are.

## Return Value

The resource’s URL, or `nil` when the edition has no such
file.