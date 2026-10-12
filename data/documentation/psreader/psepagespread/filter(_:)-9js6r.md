<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpread/filter(_:)-9js6r",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader",
      "Swift"
    ],
    "preciseIdentifier" : "s:STsE6filterySay7ElementQzGSbACqd__YKXEqd__YKs5ErrorRd__lF::SYNTHESIZED::s:8PSReader13PSEPageSpreadO"
  },
  "title" : "filter(_:)"
}
-->

# filter(_:)

```
func filter<E>(_ isIncluded: (Self.Element) throws(E) -> Bool) throws(E) -> [Self.Element] where E : Error
```