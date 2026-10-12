<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegateP"
  },
  "title" : "PaywallDelegate"
}
-->

# PaywallDelegate

A delegate protocol used to provide paywall view controllers for controlling
access to premium content within the SDK.

```
protocol PaywallDelegate
```

## Overview

By default, the SDK does **not** restrict access or display paywalls.
To enable paywall functionality, clients must implement this delegate.

## Usage

```swift
struct MyPaywallDelegate: PaywallDelegate {
    func paywallViewControllerForAction(
        openReplicaEdition edition: PSEdition
    ) -> PaywallViewController? {
        return MyPaywallVC()
    }

    func paywallViewControllerForAction(
        openFeedEdition published: PSEPublished
    ) -> PaywallViewController? {
        return MyPaywallVC()
    }
}

// Assign to global config
let globalConfig = GlobalConfiguration(
    apiKey: "KEY",
    accountGUID: "GUID",
    paywallDelegate: MyPaywallDelegate()
)
```

> Tip: The download methods default to their open counterparts, so you only
> need to override them if download access should differ from viewing access.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Paywalls>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallViewController``

## Topics

### Gating Editions

[`paywallViewControllerForAction(openFeedEdition:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openFeedEdition:))

Provides a paywall view controller displayed when attempting to open
an edition on PageSuite’s current system, classic PDF or responsive.

[`paywallViewControllerForAction(downloadFeedEdition:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(downloadFeedEdition:))

Provides a paywall view controller displayed when attempting to
download an edition on PageSuite’s current system.

### Gating Search Results

[`paywallViewControllerForAction(openSearchResult:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openSearchResult:))

Provides a paywall view controller displayed when attempting to open
an edition from a search result.

### Replica Editions

[`paywallViewControllerForAction(openReplicaEdition:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openReplicaEdition:))

Provides a paywall view controller displayed when attempting to open
an edition on the legacy replica system.

[`paywallViewControllerForAction(downloadReplicaEdition:)`](/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(downloadReplicaEdition:))

Provides a paywall view controller displayed when attempting to
download an edition on the legacy replica system.

[`PSEdition`](/documentation/PSReader/PSEdition)

An edition on PageSuite’s legacy replica system.

