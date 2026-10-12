<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -",
    "macOS: 12.0.0 -",
    "tvOS: 15.0.0 -",
    "watchOS: 8.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpread/sorted(using:)-5oq59",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader",
      "Swift"
    ],
    "preciseIdentifier" : "s:ST10FoundationE6sorted5usingSay7ElementQzGqd___tSTRd__AA14SortComparatorRd_0_ADQyd__Rsd_0_8ComparedQyd_0_AERSr0_lF::SYNTHESIZED::s:8PSReader13PSEPageSpreadO"
  },
  "title" : "sorted(using:)"
}
-->

# sorted(using:)

```
func sorted<S, Comparator>(using comparators: S) -> [Self.Element] where S : Sequence, Comparator : SortComparator, Comparator == S.Element, Self.Element == Comparator.Compared
```