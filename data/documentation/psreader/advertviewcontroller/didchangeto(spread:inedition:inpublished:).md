<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertViewController/didChangeTo(spread:inEdition:inPublished:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20AdvertViewControllerP11didChangeTo6spread9inEdition0I9PublishedyAA13PSEPageSpreadOSg_AA10PSEEditionCAA12PSEPublishedCtF"
  },
  "title" : "didChangeTo(spread:inEdition:inPublished:)"
}
-->

# didChangeTo(spread:inEdition:inPublished:)

Called by the reader for **editions on PageSuite’s current system**
when the visible page changes.

```
@MainActor func didChangeTo(spread: PSEPageSpread?, inEdition edition: PSEEdition, inPublished published: PSEPublished)
```

## Parameters

`spread`

The currently visible page spread, or `nil` if there is no
active page. Use `referencePage()` to get the primary `PSEPage`.

`edition`

The edition being viewed.

`published`

The published application context.

## Discussion

Use this to refresh your ad or update targeting based on the current
page. For example, you might use the page number for section-level
targeting:

```swift
func didChangeTo(spread: PSEPageSpread?,
                 inEdition edition: PSEEdition,
                 inPublished published: PSEPublished) {
    guard let page = spread?.referencePage() else { return }
    adView.setTargeting(page: page.pageNumber)
    adView.loadNewAd()
}
```