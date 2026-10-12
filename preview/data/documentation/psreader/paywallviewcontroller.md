<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21PaywallViewControllerP"
  },
  "title" : "PaywallViewController"
}
-->

# PaywallViewController

A view controller protocol used by the SDK to present paywalls when
accessing restricted content.

```
@MainActor protocol PaywallViewController : UIViewController
```

## Overview

Implement this protocol in a custom view controller that presents your
paywall or subscription UI. The SDK presents the view controller modally
but does not dismiss it — the view controller owns its own dismissal and
presentation style. When the paywall flow ends, dismiss the view
controller and then invoke [`onDismiss`](/documentation/PSReader/PaywallViewController/onDismiss) to tell the SDK whether to grant
access.

## Usage

```swift
class MyPaywallVC: UIViewController, PaywallViewController {
    var onDismiss: ((Bool) -> Void)?

    @objc func subscribeTapped() {
        // After successful subscription...
        dismiss(animated: true) {
            self.onDismiss?(true)
        }
    }

    @objc func cancelTapped() {
        dismiss(animated: true) {
            self.onDismiss?(false)
        }
    }
}
```

> Important: ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallViewController/onDismiss`` is a callback that signals the access decision,
> not a dismissal command. Always call `dismiss(animated:)` yourself,
> invoke ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallViewController/onDismiss`` exactly once *after* dismissal completes (the SDK
> resumes the originating action the moment the closure fires), and make
> sure it runs for any interactive dismissal your presentation style
> allows (e.g. swiping a sheet down). See <doc://com.pagesuite.PSReader/documentation/PSReader/Paywalls> for
> the recommended pattern.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Paywalls>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallDelegate``

## Topics

### Reporting the Decision

[`onDismiss`](/documentation/PSReader/PaywallViewController/onDismiss)

A continuation callback invoked upon completion of the paywall
interaction, signalling whether the SDK should grant access to the
requested content.

