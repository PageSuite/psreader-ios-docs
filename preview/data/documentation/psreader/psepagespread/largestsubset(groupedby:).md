<!--
{
  "availability" : [
    "iOS: 17.0.0 -",
    "iPadOS: 17.0.0 -",
    "macCatalyst: 17.0.0 -",
    "macOS: 14.0.0 -",
    "tvOS: 17.0.0 -",
    "visionOS: 1.0.0 -",
    "watchOS: 10.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpread/largestSubset(groupedBy:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader",
      "Swift"
    ],
    "preciseIdentifier" : "s:ST6TipKitE13largestSubset9groupedBySayAA4TipsO5EventV8DonationVy_qd___GGs7KeyPathCyqd__qd_0_G_tSeRd__SERd__s8SendableRd__SHRd_0_AJ7ElementRtzr0_lF::SYNTHESIZED::s:8PSReader13PSEPageSpreadO"
  },
  "title" : "largestSubset(groupedBy:)"
}
-->

# largestSubset(groupedBy:)

```
func largestSubset<DonationInfo, Value>(groupedBy keyPath: KeyPath<DonationInfo, Value>) -> [Self.Element] where DonationInfo : Decodable, DonationInfo : Encodable, DonationInfo : Sendable, Value : Hashable, Self.Element == Tips.Event<DonationInfo>.Donation
```