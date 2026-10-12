<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/advertProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader7PSEPageC14advertProviderAA09PSEAdvertD0OSgvp"
  },
  "title" : "advertProvider"
}
-->

# advertProvider

The provider serving this advert page, parsed from
[`advertType`](/documentation/PSReader/PSEPage/advertType); `nil` for non-advert pages and unknown
providers.

```
var advertProvider: PSEAdvertProvider? { get }
```