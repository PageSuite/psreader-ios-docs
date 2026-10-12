<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertDelegate/advertViewControllerForTopBanner(inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14AdvertDelegateP32advertViewControllerForTopBanner16inReplicaEditionAA0beF0_pSgAA9PSEditionC_tF"
  },
  "title" : "advertViewControllerForTopBanner(inReplicaEdition:)"
}
-->

# advertViewControllerForTopBanner(inReplicaEdition:)

Provides a view controller for displaying a top advert banner within
legacy replica editions.

```
@MainActor func advertViewControllerForTopBanner(inReplicaEdition edition: PSEdition) -> AdvertViewController?
```

## Parameters

`edition`

The legacy replica edition currently displayed.

## Return Value

An advert view controller or `nil` to omit displaying the advert.

## Discussion

The default implementation returns `nil`.