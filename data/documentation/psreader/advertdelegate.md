<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14AdvertDelegateP"
  },
  "title" : "AdvertDelegate"
}
-->

# AdvertDelegate

A delegate protocol to enable custom advertising placements within the SDK.

```
protocol AdvertDelegate
```

## Overview

By default, the SDK **does not** include any banner advert functionality.
To enable banner advertisements, clients **must** implement this protocol.
The provided view controllers are embedded automatically into designated
banner placements within the SDK’s reader UIs.

In addition to banners, editions can contain **full-page advert pages**
(`advert_html` / `advert_third_party`). These render out of the box using
the SDK’s built-in webview implementation; implement
[`advertViewController(forAdvertPage:inPublished:edition:)`](/documentation/PSReader/AdvertDelegate/advertViewController(forAdvertPage:inPublished:edition:)) to override
that rendering with your own view controller — required for Google Ad
Manager advert pages, which have no built-in implementation and are
otherwise left blank.

## Usage

```swift
struct MyAdvertDelegate: AdvertDelegate {
    func advertViewControllerForBottomBanner(
        inPublished published: PSEPublished,
        edition: PSEEdition
    ) -> AdvertViewController? {
        return MyBannerAdVC(adUnitID: "feed-bottom-banner")
    }
}
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertViewController``

## Topics

### Providing Banners

[`advertViewControllerForBottomBanner(inPublished:edition:)`](/documentation/PSReader/AdvertDelegate/advertViewControllerForBottomBanner(inPublished:edition:))

Provides a view controller for displaying a bottom advert banner within
editions on PageSuite’s current system.

### Replacing Advert Pages

[`advertViewController(forAdvertPage:inPublished:edition:)`](/documentation/PSReader/AdvertDelegate/advertViewController(forAdvertPage:inPublished:edition:))

Provides a view controller for rendering a **full-page advert page**
within editions on PageSuite’s current system.

### Replica Editions

[`advertViewControllerForBottomBanner(inReplicaEdition:)`](/documentation/PSReader/AdvertDelegate/advertViewControllerForBottomBanner(inReplicaEdition:))

Provides a view controller for displaying a bottom advert banner within
legacy replica editions.

[`advertViewControllerForTopBanner(inReplicaEdition:)`](/documentation/PSReader/AdvertDelegate/advertViewControllerForTopBanner(inReplicaEdition:))

Provides a view controller for displaying a top advert banner within
legacy replica editions.

