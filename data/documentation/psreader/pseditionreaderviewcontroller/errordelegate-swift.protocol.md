<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/ErrorDelegate-swift.protocol",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC13ErrorDelegateP"
  },
  "title" : "PSEditionReaderViewController.ErrorDelegate"
}
-->

# PSEditionReaderViewController.ErrorDelegate

Supplies the views shown when content fails.

```
protocol ErrorDelegate : AnyObject
```

## Overview

Both methods have localized default implementations; override to
brand them. [`PSEditionErrorView`](/documentation/PSReader/PSEditionErrorView) is the standard look and accepts
custom strings.

## Topics

### Customizing Error UI

[`genericErrorView()`](/documentation/PSReader/PSEditionReaderViewController/ErrorDelegate-swift.protocol/genericErrorView())

The view shown over a page whose assets failed to load. The
reader retries the page when the view is tapped.

[`translationErrorAlert()`](/documentation/PSReader/PSEditionReaderViewController/ErrorDelegate-swift.protocol/translationErrorAlert())

The alert presented when article translation fails.

