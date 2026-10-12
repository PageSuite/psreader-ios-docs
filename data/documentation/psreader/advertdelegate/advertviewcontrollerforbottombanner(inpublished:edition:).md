<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertDelegate/advertViewControllerForBottomBanner(inPublished:edition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14AdvertDelegateP35advertViewControllerForBottomBanner11inPublished7editionAA0beF0_pSgAA12PSEPublishedC_AA10PSEEditionCtF"
  },
  "title" : "advertViewControllerForBottomBanner(inPublished:edition:)"
}
-->

# advertViewControllerForBottomBanner(inPublished:edition:)

Provides a view controller for displaying a bottom advert banner within
editions on PageSuite’s current system.

```
@MainActor func advertViewControllerForBottomBanner(inPublished published: PSEPublished, edition: PSEEdition) -> AdvertViewController?
```

## Parameters

`published`

The published application context.

`edition`

The edition currently being viewed.

## Return Value

A configured `AdvertViewController` instance, or `nil` to omit the advert.