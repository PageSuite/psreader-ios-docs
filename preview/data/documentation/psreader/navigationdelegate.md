<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/NavigationDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18NavigationDelegateP"
  },
  "title" : "NavigationDelegate"
}
-->

# NavigationDelegate

A delegate for the prebuilt UI’s replica reader lifecycle.

```
protocol NavigationDelegate
```

## Overview

Use it to respond as legacy replica editions open and close, such as
tracking analytics or adjusting your app’s UI state. Editions on
PageSuite’s current system never call it.

```swift
struct MyNavigationDelegate: NavigationDelegate {
    func willPresentReplicaReader() {
        analytics.track("reader_opened")
    }

    func willDismissReplicaReader() {
        analytics.track("reader_closed")
    }
}
```

For the reader’s other options, see [Customizing the Reader Screen](/documentation/PSReader/Customizing-the-Reader-Screen).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/navigationDelegate``

## Topics

### Replica Editions

[`willPresentReplicaReader()`](/documentation/PSReader/NavigationDelegate/willPresentReplicaReader())

Called just before a replica edition opens, in either the modern or the
legacy replica reader.

[`willDismissReplicaReader()`](/documentation/PSReader/NavigationDelegate/willDismissReplicaReader())

Called when the legacy replica reader closes.

