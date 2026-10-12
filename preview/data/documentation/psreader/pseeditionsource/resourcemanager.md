<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEditionSource/resourceManager",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16PSEEditionSourceP15resourceManagerAA0b8ResourceE0_pvp"
  },
  "title" : "resourceManager"
}
-->

# resourceManager

Resolves the edition’s resource references to locations or data.
Defaults to a manager that reads the edition’s local cache and
fetches absolute URLs over HTTP.

```
var resourceManager: PSEEditionResourceManager { get }
```