<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertDelegate/advertViewControllerForBottomBanner(inReplicaEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14AdvertDelegateP35advertViewControllerForBottomBanner16inReplicaEditionAA0beF0_pSgAA9PSEditionC_tF"
  },
  "title" : "advertViewControllerForBottomBanner(inReplicaEdition:)"
}
-->

# advertViewControllerForBottomBanner(inReplicaEdition:)

Provides a view controller for displaying a bottom advert banner within
legacy replica editions.

```
@MainActor func advertViewControllerForBottomBanner(inReplicaEdition edition: PSEdition) -> AdvertViewController?
```

## Parameters

`edition`

The legacy replica edition currently displayed.

## Return Value

An advert view controller or `nil` to omit displaying the advert.

## Discussion

The default implementation returns `nil`, so a delegate that
implements only the methods for editions on PageSuite’s current system
shows no banners in legacy replica editions.