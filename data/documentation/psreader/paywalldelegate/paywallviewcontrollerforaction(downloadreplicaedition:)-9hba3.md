<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(downloadReplicaEdition:)-9hba3",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegatePAAE30paywallViewControllerForAction22downloadReplicaEditionAA0beF0_pSgAA9PSEditionC_tF"
  },
  "title" : "paywallViewControllerForAction(downloadReplicaEdition:)"
}
-->

# paywallViewControllerForAction(downloadReplicaEdition:)

Returns the paywall from
`PaywallDelegate/paywallViewControllerForAction(openReplicaEdition:)`,
so downloading a legacy replica edition is gated the same way as
opening it.

```
@MainActor func paywallViewControllerForAction(downloadReplicaEdition edition: PSEdition) -> PaywallViewController?
```

## Parameters

`edition`

The legacy replica edition being downloaded.

## Return Value

The paywall for opening the edition, or `nil`.