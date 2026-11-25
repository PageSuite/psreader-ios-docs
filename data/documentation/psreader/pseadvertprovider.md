<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEAdvertProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17PSEAdvertProviderO"
  },
  "title" : "PSEAdvertProvider"
}
-->

# PSEAdvertProvider

The ad-tech provider an advert page is served through.

```
enum PSEAdvertProvider
```

## Overview

Providers the SDK knows have a case of their own; any other advert type
arrives as [`PSEAdvertProvider.custom(_:)`](/documentation/PSReader/PSEAdvertProvider/custom(_:)) with the published string, so a page for a
provider only your app knows still reaches your advert delegate.

## Topics

### Built-In Rendering

[`PSEAdvertProvider.image`](/documentation/PSReader/PSEAdvertProvider/image)

A static image advert. The built-in rendering shows the image from the
page’s [`advertConfig`](/documentation/PSReader/PSEPage/advertConfig), linked when the config has a link.

[`PSEAdvertProvider.htlbid`](/documentation/PSReader/PSEAdvertProvider/htlbid)

An htlbid advert. The built-in rendering runs it in a web view through
the hosted loader that [`loaderTemplateURL`](/documentation/PSReader/PSEDefaultAdvertConfiguration/loaderTemplateURL)
names.

[`PSEAdvertProvider.aditude`](/documentation/PSReader/PSEAdvertProvider/aditude)

An Aditude advert. The built-in rendering runs it in a web view
through the hosted loader that
[`loaderTemplateURL`](/documentation/PSReader/PSEDefaultAdvertConfiguration/loaderTemplateURL) names.

### Rendered by Your App

[`PSEAdvertProvider.googleAdManager`](/documentation/PSReader/PSEAdvertProvider/googleAdManager)

A Google Ad Manager advert. These pages have no built-in rendering:
supply a view controller through [`AdvertDelegate`](/documentation/PSReader/AdvertDelegate) or
[`PSEditionReaderViewController.AdvertDelegate`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol), configured with a
[`PSEGAMAdvertConfig`](/documentation/PSReader/PSEGAMAdvertConfig).

[`PSEAdvertProvider.custom(_:)`](/documentation/PSReader/PSEAdvertProvider/custom(_:))

A provider the SDK doesn’t know, carrying the page’s advert type
lowercased, for example `custom("freestar")`; match it with a
lowercase literal. These pages have no
built-in rendering: supply a view controller through
[`AdvertDelegate`](/documentation/PSReader/AdvertDelegate) or [`PSEditionReaderViewController.AdvertDelegate`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol),
built from [`thirdPartyAdvertConfig`](/documentation/PSReader/PSEPage/thirdPartyAdvertConfig), or the reader leaves
the page out.

