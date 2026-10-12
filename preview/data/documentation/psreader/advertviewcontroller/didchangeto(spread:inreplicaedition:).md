<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertViewController/didChangeTo(spread:inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20AdvertViewControllerP11didChangeTo6spread16inReplicaEditionyAA19PSReplicaPageSpreadOSg_AA0lK0VtF"
  },
  "title" : "didChangeTo(spread:inReplicaEdition:)"
}
-->

# didChangeTo(spread:inReplicaEdition:)

Called by the modern reader for **legacy replica editions** when the
visible page changes.

```
@MainActor func didChangeTo(spread: PSReplicaPageSpread?, inReplicaEdition replicaEdition: PSReplicaEdition)
```

## Parameters

`spread`

The currently visible page spread, or `nil` if there is no
active page. Use `referencePage()` to get the primary `PSPage`.

`replicaEdition`

The legacy replica edition being viewed.

## Discussion

Use this to refresh your ad or update targeting based on the current
page. For example:

```swift
func didChangeTo(spread: PSReplicaPageSpread?,
                 inReplicaEdition replicaEdition: PSReplicaEdition) {
    guard let page = spread?.referencePage() else { return }
    adView.setTargeting(page: page.num)
    adView.loadNewAd()
}
```