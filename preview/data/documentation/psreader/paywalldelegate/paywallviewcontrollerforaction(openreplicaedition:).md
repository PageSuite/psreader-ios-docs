<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegateP30paywallViewControllerForAction18openReplicaEditionAA0beF0_pSgAA9PSEditionC_tF"
  },
  "title" : "paywallViewControllerForAction(openReplicaEdition:)"
}
-->

# paywallViewControllerForAction(openReplicaEdition:)

Provides a paywall view controller displayed when attempting to open
an edition on the legacy replica system.

```
@MainActor func paywallViewControllerForAction(openReplicaEdition edition: PSEdition) -> PaywallViewController?
```

## Parameters

`edition`

The legacy replica edition the user is
attempting to open.

## Return Value

A configured `PaywallViewController`, or `nil` if no paywall should be presented.