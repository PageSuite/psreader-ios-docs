<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEThirdPartyAdvertConfig/adUnitId",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEThirdPartyAdvertConfig(py)adUnitId"
  },
  "title" : "adUnitId"
}
-->

# adUnitId

The ad unit to request: the config’s `adUnitId`, or failing that its
`adTag`, `adzone`, `adslot` or `adUnit`, whichever the provider
publishes. `nil` when the config names none.

```
@objc var adUnitId: String?
```