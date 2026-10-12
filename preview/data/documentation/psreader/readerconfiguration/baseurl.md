<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderConfiguration/baseURL",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19ReaderConfigurationV7baseURLSSSgvp"
  },
  "title" : "baseURL"
}
-->

# baseURL

The base URL used when rendering HTML.

```
var baseURL: String?
```

## Discussion

If a page does not provide its own `baseURL`, this value is used as a
fallback when loading HTML content in the reader.

Note: When loading a `dynamicArchive` this property is overwritten with the remotely configured value.