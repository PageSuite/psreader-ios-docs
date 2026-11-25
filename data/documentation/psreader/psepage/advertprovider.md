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
[`advertType`](/documentation/PSReader/PSEPage/advertType); `nil` for pages with no advert type. A type
the SDK doesn’t know is [`PSEAdvertProvider.custom(_:)`](/documentation/PSReader/PSEAdvertProvider/custom(_:)).

```
var advertProvider: PSEAdvertProvider? { get }
```