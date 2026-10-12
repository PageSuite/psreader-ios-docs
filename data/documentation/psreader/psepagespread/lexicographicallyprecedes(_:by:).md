<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpread/lexicographicallyPrecedes(_:by:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader",
      "Swift"
    ],
    "preciseIdentifier" : "s:STsE25lexicographicallyPrecedes_2bySbqd___Sb7ElementQz_ADtKXEtKSTRd__ACQyd__ADRSlF::SYNTHESIZED::s:8PSReader13PSEPageSpreadO"
  },
  "title" : "lexicographicallyPrecedes(_:by:)"
}
-->

# lexicographicallyPrecedes(_:by:)

```
func lexicographicallyPrecedes<OtherSequence>(_ other: OtherSequence, by areInIncreasingOrder: (Self.Element, Self.Element) throws -> Bool) rethrows -> Bool where OtherSequence : Sequence, Self.Element == OtherSequence.Element
```