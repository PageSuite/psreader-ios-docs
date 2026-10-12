<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/resolve(resource:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC7resolve8resourceSSSgSS_tF"
  },
  "title" : "resolve(resource:)"
}
-->

# resolve(resource:)

Returns the key the edition’s file list holds the resource under.

```
func resolve(resource hash: String) -> String?
```

## Parameters

`hash`

The resource reference, as it appears in the
edition’s content. A reference with a path also matches by its last
component.

## Return Value

The reference itself or its last path component, or `nil`
when the edition has no such file.