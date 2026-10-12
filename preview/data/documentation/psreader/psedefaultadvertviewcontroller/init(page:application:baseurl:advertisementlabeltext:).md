<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDefaultAdvertViewController/init(page:application:baseURL:advertisementLabelText:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader30PSEDefaultAdvertViewControllerC4page11application7baseURL22advertisementLabelTextACSgAA7PSEPageC_AA11PSAppConfigCSgSSSgSStcfc"
  },
  "title" : "init(page:application:baseURL:advertisementLabelText:)"
}
-->

# init(page:application:baseURL:advertisementLabelText:)

Creates the default renderer for an advert page, or returns `nil`
when the page has nothing it can render.

```
@MainActor init?(page: PSEPage, application: PSAppConfig?, baseURL: String?, advertisementLabelText: String = "Advertisement")
```

## Parameters

`page`

The advert page to render.

`application`

The app configuration. For third-party adverts its
ad-stack scripts take precedence over the page’s own copy; pass
`nil` to use the page’s.

`baseURL`

The base URL the advert content loads against, with
`https://` assumed when it has no scheme. Without one the content
has no web origin, which blocks third-party ad serving.

`advertisementLabelText`

The label shown above fixed-size
third-party slots. Full-page adverts show no label.

## Discussion

Create one from your [`PSEditionReaderViewController.AdvertDelegate`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol)
to keep the built-in rendering while choosing its inputs, for example
a localized advertisement label: the reader’s own fallback always
labels slots “Advertisement”. The reader’s fallback takes its base
URL from your media delegate’s `baseURL(for:)`, then the app
configuration’s advert domain, then its edition base URL.

Returns `nil` for Google Ad Manager pages, third-party pages whose
provider has no hosted loader, image adverts without a valid
configuration, and pages with no content to load.