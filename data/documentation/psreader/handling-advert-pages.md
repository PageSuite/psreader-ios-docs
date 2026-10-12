<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Handling-Advert-Pages",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Handling Advert Pages"
}
-->

# Handling Advert Pages

Let the reader in your own reader screen render advert pages, or serve them from your own ad stack, and place any banners in your chrome.

## Overview

The prebuilt reader asks the app for a banner to show below the pages,
and for a view controller for each advert page. In your own reader
screen, banners are yours to build, but advert pages need little work:
[`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) renders them itself, with the same
built-in rendering, and its advert delegate can replace any of them.

Using the prebuilt UI? See [Advertisements](/documentation/PSReader/Advertisements).

When your editions carry adverts, your reader screen usually needs two
things. First, the app configuration, passed when the reader opens an
edition, so third-party adverts can serve and in-article adverts appear:
[Passing the App Configuration](/documentation/PSReader/Hosting-the-Reader#Passing-the-App-Configuration) adds an `appConfig`
property to `ReaderScreenViewController`, the reader screen from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader), and passes it to the reader. Second, a view
controller for Google Ad Manager pages, which have no built-in rendering.
In `hostReader()`, with the other delegates, make the screen the reader’s
advert delegate:

```swift
reader.advertDelegate = self
```

And conform in an extension, in the same file as the class:

```swift
extension ReaderScreenViewController: PSEditionReaderViewController.AdvertDelegate {

    func advertViewController(forPage page: PSEPage) -> PSEAdvertContentViewController? {
        guard page.advertProvider == .googleAdManager else {
            return nil   // The built-in rendering.
        }
        return GoogleAdPageViewController(page: page)
    }
}
```

`GoogleAdPageViewController` is your advert page view controller, written
as in [Rendering Advert Pages Yourself](/documentation/PSReader/Advertisements#Rendering-Advert-Pages-Yourself). In Swift 6
language mode, mark the conformance `@preconcurrency`; see
[Swift 6 Language Mode](/documentation/PSReader/Hosting-the-Reader#Swift-6-Language-Mode).

## Giving Third-Party Adverts an Origin

The built-in rendering serves third-party adverts in a web view, which
needs a web origin to load against, usually your publication’s website.
The reader takes it from your media delegate’s
[`baseURL(for:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/baseURL(for:)) when that
returns one, and otherwise from your app configuration’s advertising
domain, then its edition base URL. Third-party adverts also prefer the app
configuration’s ad-stack scripts to the page’s own copy. With neither a
base URL from your media delegate nor an app configuration, third-party
adverts have no origin and can’t serve.

The app configuration also switches on the in-article adverts it
configures, which templated pages render within their content (see
[Adverts Inside Pages](/documentation/PSReader/Advertisements#Adverts-Inside-Pages)). To load it and pass it to the
reader, see [Passing the App Configuration](/documentation/PSReader/Hosting-the-Reader#Passing-the-App-Configuration).

## Serving Advert Pages From Your Ad Stack

The reader asks
[`advertViewController(forPage:)`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol/advertViewController(forPage:))
for every `advert_html` and `advert_third_party` page. Return a view
controller that adopts [`PSEAdvertContentViewController`](/documentation/PSReader/PSEAdvertContentViewController), and the reader
pins its view to the page’s edges; return `nil` to keep the built-in
rendering for a page. To render nothing, return an empty view controller
instead. `advert` and `advert_pdf` pages render as PDF or web content and
never reach the delegate.

Set the delegate before the edition opens, as `hostReader()` does, so
the first pages use it. Everything else works as it does in the prebuilt
reader:

- The reader builds pages before they’re on screen and rebuilds them
  later, and asks your delegate each time, so return a new view controller
  from every call.
- Request ads and count impressions from the reader’s visibility hooks,
  never `viewDidAppear`. <doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements#Rendering-Advert-Pages-Yourself>
  explains each hook, with a Google Ad Manager view controller to start
  from.
- <doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements#Full-Page-Advert-Pages> lists what the built-in
  rendering shows for each provider.
- A classic PDF edition’s page-zero advert reaches your delegate too, for a
  slot beside the cover; see <doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements#Adverts-Beside-the-Cover>.

## Localizing the Advertisement Label

The built-in rendering shows a label above fixed-size third-party slots.
The reader always labels them “Advertisement”, in English. To show your
own text, create the default renderer yourself, as a
[`PSEDefaultAdvertViewController`](/documentation/PSReader/PSEDefaultAdvertViewController). Replace the delegate method with:

```swift
func advertViewController(forPage page: PSEPage) -> PSEAdvertContentViewController? {
    if page.advertProvider == .googleAdManager {
        return GoogleAdPageViewController(page: page)
    }
    return PSEDefaultAdvertViewController(
        page: page,
        application: appConfig,
        baseURL: "https://www.example.com",
        advertisementLabelText: String(localized: "Advertisement")
    )
}
```

Pass the app configuration you open the edition with, and the base URL
the advert content loads against, usually your publication’s website. The
initializer returns `nil` for pages it can’t render, such as Google Ad
Manager pages, and those pages stay blank.

## Placing a Banner

The reader has no banner slot. A banner is part of your chrome: lay it
out below the reader, as the prebuilt reader screen does, by pinning the
reader’s bottom edge to the banner’s top in `hostReader()` instead of to
the safe area. Add a property that remembers the page the banner last
targeted:

```swift
private var bannerPageGUID: String?
```

And in `updateChrome()`, refresh the banner when the reader settles on a
new page:

```swift
if page.pageguid != bannerPageGUID {
    bannerPageGUID = page.pageguid
    bannerAd.refresh(section: page.section)
}
```

`bannerAd` is your banner view. The check skips a settle on the same
page, which the reader reports when the user drags and lets go without
turning the page.

## Handling Clickthroughs and Analytics

The built-in rendering doesn’t navigate an advert’s web view when the user
taps it. Clickthroughs, including `window.open` calls, post
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification), and open only
once your reader screen observes it, as it does for every other link; see
[Opening Links](/documentation/PSReader/Handling-Media-and-Link-Taps#Opening-Links).

The prebuilt reader reports an advert page that settles on screen as a
page view. Its analytics events don’t fire in your reader screen;
[Reporting Page Views](/documentation/PSReader/Reporting-Analytics#Reporting-Page-Views) reports page views and
says how to decide whether advert pages count. Count impressions in your
own advert view controllers.

## Topics

### Localizing the Advertisement Label

[`PSEDefaultAdvertViewController`](/documentation/PSReader/PSEDefaultAdvertViewController)

The framework’s default, webview-only renderer for advert pages
(`advert_html` / `advert_third_party`). No third-party native SDKs are
involved — third-party ad tech (htlbid/aditude) runs inside the webview
via the PageSuite hosted loader. Google Ad Manager pages have no
framework default: clients supply a native Google ad through
`PSEditionReaderViewController.AdvertDelegate.advertViewController(forPage:)`. This class is
public so overriding delegates can still fall back to it selectively.

