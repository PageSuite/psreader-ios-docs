<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionPageViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27PSEditionPageViewControllerP"
  },
  "title" : "PSEditionPageViewController"
}
-->

# PSEditionPageViewController

A view controller the reader pages between — one per spread.

```
@MainActor protocol PSEditionPageViewController : UIViewController
```

## Overview

The reader supplies its own implementations for PDF, HTML, and advert
content; [`currentPageViewController()`](/documentation/PSReader/PSEditionReaderViewController/currentPageViewController())
returns the one on screen. The lifecycle methods are driven by the
pager’s visibility tracking, which is more precise than UIKit appearance
callbacks for preloaded pages.

## Topics

### Position

[`index`](/documentation/PSReader/PSEditionPageViewController/index)

The spread index this controller currently represents.

### Responding to Visibility

[`pageInView()`](/documentation/PSReader/PSEditionPageViewController/pageInView())

The page became the current page.

[`pageOutOfView()`](/documentation/PSReader/PSEditionPageViewController/pageOutOfView())

The page stopped being the current page (or was preloaded and never
shown).

[`didEndDecelerating()`](/documentation/PSReader/PSEditionPageViewController/didEndDecelerating())

The pager’s scroll deceleration ended with this page current.

### Responding to Layout

[`layout()`](/documentation/PSReader/PSEditionPageViewController/layout())

The pager completed a layout pass.

[`heightDidChange()`](/documentation/PSReader/PSEditionPageViewController/heightDidChange())

The page’s content height changed.

### Reloading and Reuse

[`reloadPage()`](/documentation/PSReader/PSEditionPageViewController/reloadPage())

Re-render the page’s content in place.

[`prepareForReuse()`](/documentation/PSReader/PSEditionPageViewController/prepareForReuse())

The controller is returning to the reuse pool; tear down content.

