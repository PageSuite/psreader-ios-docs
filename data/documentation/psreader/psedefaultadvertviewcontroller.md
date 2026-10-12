<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDefaultAdvertViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEDefaultAdvertViewController"
  },
  "title" : "PSEDefaultAdvertViewController"
}
-->

# PSEDefaultAdvertViewController

The framework’s default, webview-only renderer for advert pages
(`advert_html` / `advert_third_party`). No third-party native SDKs are
involved — third-party ad tech (htlbid/aditude) runs inside the webview
via the PageSuite hosted loader. Google Ad Manager pages have no
framework default: clients supply a native Google ad through
`PSEditionReaderViewController.AdvertDelegate.advertViewController(forPage:)`. This class is
public so overriding delegates can still fall back to it selectively.

```
@MainActor final class PSEDefaultAdvertViewController
```

## Overview

Fixed-size slots (hosted loader) show an “Advertisement” label above the
ad; full-page flows render label-free. The label text is injected
through the initializer so callers control its localization (the
prebuilt UI passes its `LocalizationManager` string).

Serving is gated on the pager’s visibility hooks: nothing that can fire
an impression happens until the page is actually the current page.

Advert clickthroughs, including `window.open` calls, post
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification) instead of
navigating the advert.

To keep or replace it in your own reader screen, see
[Handling Advert Pages](/documentation/PSReader/Handling-Advert-Pages).

## Topics

### Creating the Renderer

[`init(page:application:baseURL:advertisementLabelText:)`](/documentation/PSReader/PSEDefaultAdvertViewController/init(page:application:baseURL:advertisementLabelText:))

Creates the default renderer for an advert page, or returns `nil`
when the page has nothing it can render.

### Responding to Visibility

[`advertPageInView()`](/documentation/PSReader/PSEDefaultAdvertViewController/advertPageInView())

Marks the page as current and starts the advert once its content is
ready. Nothing that can fire an impression runs before the first
call.

[`advertPageOutOfView()`](/documentation/PSReader/PSEDefaultAdvertViewController/advertPageOutOfView())

Marks the page as no longer current. A third-party slot that has
served is destroyed and reloaded, so the next visit serves a fresh
advert.

### Responding to Layout

[`advertLayout()`](/documentation/PSReader/PSEDefaultAdvertViewController/advertLayout())

Resizes a fixed-size third-party slot to the space available.
Full-page adverts need no work.

### Tearing Down

[`advertPrepareForReuse()`](/documentation/PSReader/PSEDefaultAdvertViewController/advertPrepareForReuse())

Cancels any pending content fetch, destroys a served third-party
slot, and empties the web view.

