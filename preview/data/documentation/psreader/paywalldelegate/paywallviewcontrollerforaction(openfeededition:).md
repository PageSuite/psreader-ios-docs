<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openFeedEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegateP30paywallViewControllerForAction15openFeedEditionAA0beF0_pSgAA12PSEPublishedC_tF"
  },
  "title" : "paywallViewControllerForAction(openFeedEdition:)"
}
-->

# paywallViewControllerForAction(openFeedEdition:)

Provides a paywall view controller displayed when attempting to open
an edition on PageSuite’s current system, classic PDF or responsive.

```
@MainActor func paywallViewControllerForAction(openFeedEdition published: PSEPublished) -> PaywallViewController?
```

## Parameters

`published`

The edition being accessed.

## Return Value

A configured `PaywallViewController`, or `nil` if no paywall is needed.