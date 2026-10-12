<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertDelegate/advertViewController(forAdvertPage:inPublished:edition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14AdvertDelegateP20advertViewController03forB4Page11inPublished7editionAA016PSEAdvertContenteF0_pSgAA7PSEPageC_AA12PSEPublishedCAA10PSEEditionCtF"
  },
  "title" : "advertViewController(forAdvertPage:inPublished:edition:)"
}
-->

# advertViewController(forAdvertPage:inPublished:edition:)

Provides a view controller for rendering a **full-page advert page**
within editions on PageSuite’s current system.

```
@MainActor func advertViewController(forAdvertPage page: PSEPage, inPublished published: PSEPublished, edition: PSEEdition) -> PSEAdvertContentViewController?
```

## Parameters

`page`

The advert page to render. Inspect `advertProvider` and
`advertConfig` for the advert’s configuration, and `isPageZero`
for the cover-spread placement.

`published`

The published application context.

`edition`

The edition currently being viewed.

## Return Value

A view controller conforming to
`PSEAdvertContentViewController`, or `nil` to use the SDK’s
built-in rendering.

## Discussion

Editions can contain dedicated advert pages (`advert_html` /
`advert_third_party`). The SDK calls this method each time the pager
builds an advert page, which happens again when the page comes back
into range and after a rotation, so return a new view controller from
every call. It covers both placements:

- **Regular advert pages** — your view controller fills the entire
  page slot.
- **The page-zero position** (`page.isPageZero`) — in double-page
  mode the advert is rendered beside the cover; the SDK sizes and
  positions your view controller inside the mirrored cover slot
  automatically.

Return `nil` to accept the SDK’s built-in webview rendering (the
PageSuite hosted loader for htlbid/aditude adverts, the advert’s own
HTML template, or image creatives). To render nothing for a page,
return an empty view controller instead of `nil`.

> Important: Google Ad Manager advert pages
> (`page.advertProvider == .googleAdManager`) have **no** built-in
> rendering — they are left blank unless this method supplies a view
> controller (for example, one hosting a native Google Mobile Ads
> banner).

> Note: The pager preloads pages while they are still off screen, so
> UIKit appearance callbacks like `viewDidAppear` fire before the
> advert is actually visible. Gate ad requests and impression
> tracking on `PSEAdvertContentViewController.advertPageInView()`,
> and tear down on `advertPageOutOfView()` /
> `advertPrepareForReuse()`.

## Usage

```swift
func advertViewController(
    forAdvertPage page: PSEPage,
    inPublished published: PSEPublished,
    edition: PSEEdition
) -> PSEAdvertContentViewController? {
    switch page.advertProvider {
    case .googleAdManager:
        return MyGAMPageAdVC(config: page.advertConfig)
    default:
        return nil // built-in webview rendering
    }
}
```

A default implementation returning `nil` is provided, so existing
delegates keep the SDK’s built-in rendering without changes.