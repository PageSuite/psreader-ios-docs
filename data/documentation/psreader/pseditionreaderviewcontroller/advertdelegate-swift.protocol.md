<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14AdvertDelegateP"
  },
  "title" : "PSEditionReaderViewController.AdvertDelegate"
}
-->

# PSEditionReaderViewController.AdvertDelegate

Overrides how advert pages render.

```
protocol AdvertDelegate : AnyObject
```

## Overview

Without a delegate the reader renders adverts with its built-in
[`PSEDefaultAdvertViewController`](/documentation/PSReader/PSEDefaultAdvertViewController), which covers HTML and image
creatives. Provide a delegate to serve adverts from your own stack
(for example Google Ad Manager).

To serve advert pages from your own reader screen, see
[Handling Advert Pages](/documentation/PSReader/Handling-Advert-Pages).

## Topics

### Rendering Advert Pages

[`advertViewController(forPage:)`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol/advertViewController(forPage:))

The view controller to render an advert page, or `nil` to accept
the built-in rendering. To render nothing for a page, return an
empty view controller.

