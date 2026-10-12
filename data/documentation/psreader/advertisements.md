<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Advertisements",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Advertisements"
}
-->

# Advertisements

Show banner adverts in the prebuilt reader, and serve its advert pages
from your own ad stack.

## Overview

The prebuilt reader shows two kinds of advert, and your
[`AdvertDelegate`](/documentation/PSReader/AdvertDelegate) supplies both. Building a custom UI? See
[Handling Advert Pages](/documentation/PSReader/Handling-Advert-Pages).

- **Banners** are view controllers you supply. The reader embeds one
  below the pages.
- **Advert pages** are part of an edition’s content. The publisher
  places them in the page flow, and users page through them like any
  other page.

Pass the delegate when you create your global configuration. Every
prebuilt reader asks it for a bottom banner and for each advert page,
whether the carousel opened the reader or one of your own screens did:

```swift
final class AppAdverts: AdvertDelegate {

    func advertViewControllerForBottomBanner(inPublished published: PSEPublished,
                                             edition: PSEEdition) -> AdvertViewController? {
        BannerAdViewController()
    }

    func advertViewController(forAdvertPage page: PSEPage,
                              inPublished published: PSEPublished,
                              edition: PSEEdition) -> PSEAdvertContentViewController? {
        guard page.advertProvider == .googleAdManager else {
            return nil   // the built-in rendering
        }
        return GoogleAdPageViewController(page: page)
    }
}

let globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID",
    advertDelegate: AppAdverts()
)
```

`BannerAdViewController` is your banner (see [Prebuilt Banners](/documentation/PSReader/Advertisements#Prebuilt-Banners)), and
`GoogleAdPageViewController` is your advert page view controller (see
[Rendering Advert Pages Yourself](/documentation/PSReader/Advertisements#Rendering-Advert-Pages-Yourself)). Return `nil` from the banner
method to show no banner.

Advert pages render out of the box, so most apps implement the page method
for one reason: Google Ad Manager pages stay blank until you supply a view
controller that requests the ad, typically with the Google Mobile Ads SDK.
The same method can replace the built-in rendering of other advert pages
too. [`isAdvertPage`](/documentation/PSReader/PSEPage/isAdvertPage) is `true` for advert pages, and
[`advertProvider`](/documentation/PSReader/PSEPage/advertProvider) names the ad technology that serves each one.

## Prebuilt Banners

The prebuilt reader asks your delegate for a banner each time it opens an
edition, and embeds the view controller you return as a child below the
pages. Return a new view controller from each call; every reader keeps its
own.

![The prebuilt reader on an edition's front page, with a placeholder banner from the app's advert delegate below the page.](images/com.pagesuite.PSReader/adverts-reader-banner~dark@2x.png)

Adopt [`AdvertViewController`](/documentation/PSReader/AdvertViewController) in a `UIViewController` subclass. The banner
is as tall as its view’s Auto Layout constraints make it, so give the view
a height constraint or an intrinsic content size:

```swift
final class BannerAdViewController: UIViewController, AdvertViewController {

    private var lastPageGUID: String?

    override func viewDidLoad() {
        super.viewDidLoad()
        view.heightAnchor.constraint(equalToConstant: 66).isActive = true
        // Add your ad view.
    }

    func didChangeTo(spread: PSEPageSpread?,
                     inEdition edition: PSEEdition,
                     inPublished published: PSEPublished) {
        guard let page = spread?.referencePage(), page.pageguid != lastPageGUID else { return }
        lastPageGUID = page.pageguid
        refreshAd(section: page.section)
    }

    private func refreshAd(section: String?) {
        // Request a new ad, targeted at the page's section.
    }
}
```

The reader calls
[`didChangeTo(spread:inEdition:inPublished:)`](/documentation/PSReader/AdvertViewController/didChangeTo(spread:inEdition:inPublished:)) each
time it settles on a page, starting with the page it opens on, and again
when the user lets go on the same page. The spread’s
[`referencePage()`](/documentation/PSReader/PSEPageSpread/referencePage()) prefers editorial content over an advert
beside it. The method does nothing unless you implement it.

> Replica: Replica readers take their bottom banner from
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertDelegate/advertViewControllerForBottomBanner(inReplicaEdition:)``,
> and also ask for a top banner, from
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertDelegate/advertViewControllerForTopBanner(inReplicaEdition:)``,
> which sits between the navigation bar and the pages. Both return `nil`
> unless you implement them. With a top banner, the replica reader’s
> navigation bar stays in place instead of hiding as the user scrolls.
> Replica readers report page changes through
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertViewController/didChangeTo(spread:inReplicaEdition:)``, or
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertViewController/didChangeToIndex(_:)`` in the legacy replica
> reader; both do nothing by default.

## Full-Page Advert Pages

Editions use four advert page types, and the reader treats them in two
ways:

- `advert_html` and `advert_third_party` pages go through advert
  rendering: your delegate first, then the built-in rendering.
- `advert` and `advert_pdf` pages render like other content pages, as web
  or PDF content, and never reach your delegate.

The built-in rendering depends on the page’s provider:

|Advert page                                                                                                                                                        |Built-in rendering                                                                                                                                                      |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|`advert_html` without a provider or configuration                                                                                                                  |The page’s HTML, or its external URL, filling the page.                                                                                                                 |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEAdvertProvider/image``                                                                                    |The image from the page’s ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/advertConfig``, fitted to the page and linked when the configuration has a link.|
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEAdvertProvider/htlbid``, ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEAdvertProvider/aditude``|A fixed-size ad slot under an advertisement label, served in a web view through a hosted loader.                                                                        |
|``doc://com.pagesuite.PSReader/documentation/PSReader/PSEAdvertProvider/googleAdManager``                                                                          |Nothing. The page stays blank unless your delegate supplies a view controller.                                                                                          |

A third-party page whose provider the SDK doesn’t recognize renders
nothing either. The hosted-loader providers also read your app
configuration: its ad-stack scripts take precedence over the page’s own
copy, and when neither the page nor [`baseURL`](/documentation/PSReader/ReaderConfiguration/baseURL) has a
base URL, its advert domain gives the page the web origin ad serving
needs. A dynamic archive provides the configuration; elsewhere, set it as
[The App Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration) shows.

The built-in rendering loads nothing that could count an impression until
the page is on screen. When a third-party slot that has served leaves the
screen, it reloads, so the next visit shows a fresh advert. Clickthroughs,
including `window.open` calls, open like other links in the reader: web
links in a Safari view controller (see [Links](/documentation/PSReader/Media-and-Links#Links)).

To serve a Google Ad Manager page, build a [`PSEGAMAdvertConfig`](/documentation/PSReader/PSEGAMAdvertConfig) from the
page’s [`advertConfig`](/documentation/PSReader/PSEPage/advertConfig). It carries the ad zone, ad section, and
sizes to request, as the sample in the next section shows.

[`loaderTemplateURL`](/documentation/PSReader/PSEDefaultAdvertConfiguration/loaderTemplateURL) returns the hosted
loader the built-in rendering uses for each third-party provider. You
rarely need to change it. Returning `nil` for a provider switches off its
built-in rendering, so its pages stay blank unless your delegate supplies
a view controller. Set it before you open an edition.

## Rendering Advert Pages Yourself

Return a view controller that adopts [`PSEAdvertContentViewController`](/documentation/PSReader/PSEAdvertContentViewController)
from your delegate’s
[`advertViewController(forAdvertPage:inPublished:edition:)`](/documentation/PSReader/AdvertDelegate/advertViewController(forAdvertPage:inPublished:edition:)),
and the reader pins its view to the page’s edges. Return `nil` to keep the
built-in rendering for a page; to render nothing, return an empty view
controller instead.

The reader builds pages before they’re on screen, and rebuilds them when
they come back into range, after a rotation, and after a reload. It asks
your delegate each time, so return a new view controller from every call.

Because pages are built off screen, `viewDidAppear` fires before the advert
is visible. Don’t request ads or count impressions there. The reader calls
these hooks instead, and each does nothing unless you implement it:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEAdvertContentViewController/advertPageInView()``: the page became
  the current page. Start or resume the ad. It can run more than once for
  one visit, so make it idempotent.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEAdvertContentViewController/advertPageOutOfView()``: the page is no
  longer current. Pause the ad. It also runs for preloaded pages that were
  never shown.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEAdvertContentViewController/advertPrepareForReuse()``: the reader is
  discarding the page. Tear the ad down completely.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEAdvertContentViewController/advertLayout()``: a layout pass
  finished, for example after a rotation or a slot resize. Fit the ad to
  the new size.

A Google Ad Manager page, ready for your Google Mobile Ads code:

```swift
final class GoogleAdPageViewController: UIViewController, PSEAdvertContentViewController {

    private let config: PSEGAMAdvertConfig

    init(page: PSEPage) {
        config = PSEGAMAdvertConfig(dictionary: page.advertConfig ?? [:])
        super.init(nibName: nil, bundle: nil)
    }

    required init?(coder: NSCoder) { fatalError("init(coder:) is not supported") }

    func advertPageInView() {
        // Request the ad for config.adZone, config.adSection, and config.sizes,
        // or resume it. Can run more than once per visit.
    }

    func advertPageOutOfView() {
        // Pause the ad, and stop counting the impression.
    }

    func advertPrepareForReuse() {
        // Destroy the ad view.
    }

    func advertLayout() {
        // Fit the ad to the view's bounds.
    }
}
```

## Changing Adverts for One Reader

Configurations copy the delegate when you create them (see
[Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI)), so set it on the global configuration
first. To change the adverts in one reader, set
[`advertDelegate`](/documentation/PSReader/ReaderConfiguration/advertDelegate) on that reader’s configuration:
the `readerConfig` of a carousel section or prebuilt screen, or the
reader configuration you pass to [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController):

```swift
// A carousel section without banners; its advert pages keep the built-in rendering
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.advertDelegate = nil

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE", config: archiveConfig)
    ]
)

// A reader with adverts of its own
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.advertDelegate = SponsoredAdverts()

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    readerConfig: readerConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
```

## The Advertisement Label

The built-in rendering shows a label above fixed-size third-party slots;
full-page adverts have none. The label’s text is the
[`LocalizedStringKey.advertisementLabel`](/documentation/PSReader/LocalizedStringKey/advertisementLabel) string, “Advertisement” by
default, and you localize it like the SDK’s other strings; see
[Localization](/documentation/PSReader/Localization).

## Adverts Beside the Cover

A classic PDF edition can open with an advert at the page-zero position
([`isPageZero`](/documentation/PSReader/PSEPage/isPageZero)). In double-page mode it sits beside the cover, in
a slot the reader sizes to mirror the cover; in single-page mode the reader
leaves it out.

A page-zero `advert_html` or `advert_third_party` page goes through your
delegate like any other advert page. The reader calls
[`advertLayout()`](/documentation/PSReader/PSEAdvertContentViewController/advertLayout()) as the cover’s size
settles, so fit the ad there. To tell the cover slot from a full page,
check whether your view controller’s parent adopts
[`PSECoverSpreadAdvertHost`](/documentation/PSReader/PSECoverSpreadAdvertHost) once it’s embedded:

```swift
override func didMove(toParent parent: UIViewController?) {
    super.didMove(toParent: parent)
    isBesideCover = parent is PSECoverSpreadAdvertHost
}
```

A page-zero `advert_pdf` page renders as a PDF beside the cover.

## Adverts Inside Pages

Templated pages can also show adverts within their content: the advert
slots listed in [`adverts`](/documentation/PSReader/PSEPage/adverts), each a [`PSEAdvert`](/documentation/PSReader/PSEAdvert), and in-article
adverts from your app configuration’s advertising settings. The page
renders both itself, without a delegate.

In-article adverts appear only when the reader has your app
configuration. Readers opened from a dynamic archive, or with
[`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController)’s shortcode initializer, load it themselves;
for other readers, set [`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig) as
[The App Configuration](/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration) shows.

## Topics

### Supplying Adverts and Banners

[`AdvertDelegate`](/documentation/PSReader/AdvertDelegate)

A delegate protocol to enable custom advertising placements within the SDK.

[`AdvertViewController`](/documentation/PSReader/AdvertViewController)

A protocol representing a view controller used for displaying banner
advertisements in the prebuilt reader.

### Advert Pages

[`PSEAdvertProvider`](/documentation/PSReader/PSEAdvertProvider)

The ad-tech provider an advert page is served through.

[`PSEGAMAdvertConfig`](/documentation/PSReader/PSEGAMAdvertConfig)

Google Ad Manager native advert configuration.

[`PSEDefaultAdvertConfiguration`](/documentation/PSReader/PSEDefaultAdvertConfiguration)

Overridable defaults for the framework-provided advert renderer.

[`PSEAdvertContentViewController`](/documentation/PSReader/PSEAdvertContentViewController)

Adopted by view controllers embedded in an advert page slot (returned from
`PSEditionReaderViewController.AdvertDelegate.advertViewController(forPage:)` or the framework
default). The pager preloads pages off screen, so UIKit appearance
callbacks fire before a page is actually visible — these hooks are driven
by the pager’s own visibility tracking instead. Gate ad serving and
impression tracking on them, never on `viewDidAppear`.

### Adverts Beside the Cover

[`PSECoverSpreadAdvertHost`](/documentation/PSReader/PSECoverSpreadAdvertHost)

Marks the reader’s container for an advert that shares the cover’s spread
(the page-zero position beside the cover in double-page mode).

### Adverts Inside Pages

[`PSEAdvert`](/documentation/PSReader/PSEAdvert)

An advert slot placed on a page or within an article.

