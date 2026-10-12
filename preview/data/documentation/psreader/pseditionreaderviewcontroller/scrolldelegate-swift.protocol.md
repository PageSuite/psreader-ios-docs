<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14ScrollDelegateP"
  },
  "title" : "PSEditionReaderViewController.ScrollDelegate"
}
-->

# PSEditionReaderViewController.ScrollDelegate

Reports the reader’s paging and zoom activity.

```
protocol ScrollDelegate : AnyObject
```

## Overview

Page indices are spread indices for the active [`PSEditionPagingMode`](/documentation/PSReader/PSEditionPagingMode)
— in double-page mode one index covers two pages. This is the hook
for page-view analytics and for keeping external UI (progress bars,
page browsers) in sync.

## Topics

### Tracking Page Changes

[`willScrollTo(pageIndex:pagingMode:source:)`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/willScrollTo(pageIndex:pagingMode:source:))

Called before the reader moves to a page, whether from a user
swipe or a `scrollTo` call. Programmatic navigation forwards the
`source` token passed to `scrollTo`; user swipes report `nil`.

[`didSettleOn(pageIndex:pagingMode:)`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/didSettleOn(pageIndex:pagingMode:))

Called when a page finishes settling on screen. Fire page-view
analytics from here.

[`pageDragged(fromPageIndex:toPageIndex:fractionComplete:pagingMode:)`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/pageDragged(fromPageIndex:toPageIndex:fractionComplete:pagingMode:))

Called continuously while the user drags between pages, with
`fractionComplete` running 0…1.

### Tracking Zoom

[`didZoom(toScale:pageIndex:pagingMode:)`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol/didZoom(toScale:pageIndex:pagingMode:))

Called when a zoom gesture on a PDF page ends (not continuously
during the pinch). Optional — defaults to a no-op.

