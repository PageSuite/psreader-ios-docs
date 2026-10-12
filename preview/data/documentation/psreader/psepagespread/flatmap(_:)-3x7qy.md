<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpread/flatMap(_:)-3x7qy",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader",
      "Swift"
    ],
    "preciseIdentifier" : "s:STsE7flatMapySay7ElementQyd__Gqd__ABQzKXEKSTRd__lF::SYNTHESIZED::s:8PSReader13PSEPageSpreadO"
  },
  "title" : "flatMap(_:)"
}
-->

# flatMap(_:)

```
func flatMap<SegmentOfResult>(_ transform: (Self.Element) throws -> SegmentOfResult) rethrows -> [SegmentOfResult.Element] where SegmentOfResult : Sequence
```