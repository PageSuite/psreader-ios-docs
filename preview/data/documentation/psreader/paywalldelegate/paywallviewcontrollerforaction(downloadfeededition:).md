<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(downloadFeedEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegateP30paywallViewControllerForAction19downloadFeedEditionAA0beF0_pSgAA12PSEPublishedC_tF"
  },
  "title" : "paywallViewControllerForAction(downloadFeedEdition:)"
}
-->

# paywallViewControllerForAction(downloadFeedEdition:)

Provides a paywall view controller displayed when attempting to
download an edition on PageSuite’s current system.

```
@MainActor func paywallViewControllerForAction(downloadFeedEdition published: PSEPublished) -> PaywallViewController?
```

## Parameters

`published`

The edition being downloaded.

## Return Value

A configured `PaywallViewController`, or `nil` if no paywall is required.

## Discussion

By default, this method delegates to `openFeedEdition` unless explicitly overridden.