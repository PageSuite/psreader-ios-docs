<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEAdvertContentViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader30PSEAdvertContentViewControllerP"
  },
  "title" : "PSEAdvertContentViewController"
}
-->

# PSEAdvertContentViewController

Adopted by view controllers embedded in an advert page slot (returned from
`PSEditionReaderViewController.AdvertDelegate.advertViewController(forPage:)` or the framework
default). The pager preloads pages off screen, so UIKit appearance
callbacks fire before a page is actually visible — these hooks are driven
by the pager’s own visibility tracking instead. Gate ad serving and
impression tracking on them, never on `viewDidAppear`.

```
@MainActor protocol PSEAdvertContentViewController : UIViewController
```

## Topics

### Responding to Visibility

[`advertPageInView()`](/documentation/PSReader/PSEAdvertContentViewController/advertPageInView())

The page became the current page. May fire repeatedly for the same
visit — implementations must be idempotent.

[`advertPageOutOfView()`](/documentation/PSReader/PSEAdvertContentViewController/advertPageOutOfView())

The page is no longer the current page. Also fires for preloaded
pages that were never shown — implementations must be idempotent.

### Responding to Layout

[`advertLayout()`](/documentation/PSReader/PSEAdvertContentViewController/advertLayout())

The host completed a layout pass (rotation, slot resize).

### Tearing Down

[`advertPrepareForReuse()`](/documentation/PSReader/PSEAdvertContentViewController/advertPrepareForReuse())

The host is returning to the reuse pool; tear down fully
(destroy ad slots, stop the webview).

