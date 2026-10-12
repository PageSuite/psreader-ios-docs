<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/Layout/init(string:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC6LayoutO6stringAESgSSSg_tcfc"
  },
  "title" : "init(string:)"
}
-->

# init(string:)

Creates a `Layout` from a string value.

```
init?(string: String?)
```

## Parameters

`string`

The string to parse into a layout type.

## Return Value

A `Layout` if the string matches “single” or “kiosk” (case-insensitive), otherwise `nil`.