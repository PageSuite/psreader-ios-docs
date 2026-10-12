<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEditionSource/resourceManager-cgjx",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16PSEEditionSourcePAAE15resourceManagerAA0b8ResourceE0_pvp"
  },
  "title" : "resourceManager"
}
-->

# resourceManager

Returns a manager backed by the edition’s local cache directory.

```
var resourceManager: PSEEditionResourceManager { get }
```

## Discussion

It resolves a reference to its file in that directory, or to `nil`
when no such file exists, and reads cached bytes from there. Absolute
`http` URLs resolve to themselves.