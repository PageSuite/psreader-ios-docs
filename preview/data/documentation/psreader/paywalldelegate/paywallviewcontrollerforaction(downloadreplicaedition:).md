<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(downloadReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegateP30paywallViewControllerForAction22downloadReplicaEditionAA0beF0_pSgAA9PSEditionC_tF"
  },
  "title" : "paywallViewControllerForAction(downloadReplicaEdition:)"
}
-->

# paywallViewControllerForAction(downloadReplicaEdition:)

Provides a paywall view controller displayed when attempting to
download an edition on the legacy replica system.

```
@MainActor func paywallViewControllerForAction(downloadReplicaEdition edition: PSEdition) -> PaywallViewController?
```

## Parameters

`edition`

The legacy replica edition being downloaded.

## Return Value

A configured `PaywallViewController`, or `nil` if no paywall is required.

## Discussion

By default, this method delegates to `openReplicaEdition` unless explicitly overridden.