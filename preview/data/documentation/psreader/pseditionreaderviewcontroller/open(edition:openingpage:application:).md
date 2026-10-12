<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC4open7edition11openingPage11applicationyAA16PSEEditionSource_p_AA7PSEPageCSgAA11PSAppConfigCSgtF"
  },
  "title" : "open(edition:openingPage:application:)"
}
-->

# open(edition:openingPage:application:)

Loads an edition into the reader, replacing any edition currently
open.

```
@MainActor func open(edition: PSEEditionSource, openingPage: PSEPage? = nil, application: PSAppConfig? = nil)
```

## Parameters

`edition`

The source to present. Obtain one from
[`openEditionSource(onProgress:)`](/documentation/PSReader/PSEPublished/openEditionSource(onProgress:)) or construct a
specific [`PSEEditionSource`](/documentation/PSReader/PSEEditionSource) yourself.

`openingPage`

The page to land on, or `nil` for the front.

`application`

The app configuration from the PageSuite portal, or
`nil`. Most reader screens don’t need it. In-article adverts,
advert pages served through a third-party ad loader, and article
widgets read their settings from it; load it with
[`AppConfigService`](/documentation/PSReader/AppConfigService) if your editions use them. The masthead
logo comes from [`editionLogoURL(for:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/editionLogoURL(for:)) instead.