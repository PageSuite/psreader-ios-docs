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
  "identifier" : "/documentation/PSReader/PSEPageSpread/donatedWithin(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader",
      "Swift"
    ],
    "preciseIdentifier" : "s:ST6TipKitE13donatedWithinySayAA4TipsO5EventV8DonationVy_qd___GGAD0G9TimeRangeVSeRd__SERd__s8SendableRd__AI7ElementRtzlF::SYNTHESIZED::s:8PSReader13PSEPageSpreadO"
  },
  "title" : "donatedWithin(_:)"
}
-->

# donatedWithin(_:)

```
func donatedWithin<DonationInfo>(_ timeRange: Tips.DonationTimeRange) -> [Self.Element] where DonationInfo : Decodable, DonationInfo : Encodable, DonationInfo : Sendable, Self.Element == Tips.Event<DonationInfo>.Donation
```