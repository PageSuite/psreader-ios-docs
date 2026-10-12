<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionErrorView",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEditionErrorView"
  },
  "title" : "PSEditionErrorView"
}
-->

# PSEditionErrorView

The standard page-failure view: a message with a tap-to-retry hint.

```
@MainActor class PSEditionErrorView
```

## Overview

The default [`PSEditionReaderViewController.ErrorDelegate`](/documentation/PSReader/PSEditionReaderViewController/ErrorDelegate-swift.protocol) shows this
with localized strings; custom delegates can reuse the look with their
own strings.

To handle page failures in your own reader screen, see
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader).

## Topics

### Creating the View

[`init(messageText:tapToRetryText:)`](/documentation/PSReader/PSEditionErrorView/init(messageText:tapToRetryText:))

Creates the view with a failure message and a retry hint.

