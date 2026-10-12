<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(downloadFeedEdition:)-740ka",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegatePAAE30paywallViewControllerForAction19downloadFeedEditionAA0beF0_pSgAA12PSEPublishedC_tF"
  },
  "title" : "paywallViewControllerForAction(downloadFeedEdition:)"
}
-->

# paywallViewControllerForAction(downloadFeedEdition:)

Returns the paywall from
`PaywallDelegate/paywallViewControllerForAction(openFeedEdition:)`,
so downloading an edition is gated the same way as opening it.

```
@MainActor func paywallViewControllerForAction(downloadFeedEdition published: PSEPublished) -> PaywallViewController?
```

## Parameters

`published`

The edition being downloaded.

## Return Value

The paywall for opening the edition, or `nil`.