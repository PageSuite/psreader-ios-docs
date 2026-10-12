<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20AdvertViewControllerP"
  },
  "title" : "AdvertViewController"
}
-->

# AdvertViewController

A protocol representing a view controller used for displaying banner
advertisements in the prebuilt reader.

```
@MainActor protocol AdvertViewController : PSBannerContent
```

## Overview

Your advert view controller is embedded as a child view controller within
the SDK’s reader interface using standard UIKit containment.

### PSBannerContent

`AdvertViewController` inherits from `PSBannerContent`, which defines a
legacy [`didChangeToIndex(_:)`](/documentation/PSReader/AdvertViewController/didChangeToIndex(_:)) callback. Only the legacy replica reader
calls it (see [`useLegacyReplicaReader`](/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader)); the reader for
editions on PageSuite’s current system and the modern replica reader don’t.

## Page Change Callbacks

The SDK calls your view controller’s page change methods as the user
navigates through an edition. Use these callbacks to refresh ad content or
update section-level ad targeting.

Each reader type calls a different method:

|Reader                                |Method                                                                                                                   |
|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
|Editions on PageSuite’s current system|``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertViewController/didChangeTo(spread:inEdition:inPublished:)``  |
|Legacy replica editions, modern reader|``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertViewController/didChangeTo(spread:inReplicaEdition:)``       |
|Legacy replica editions, legacy reader|``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertViewController/didChangeToIndex(_:)`` (via `PSBannerContent`)|

All three have default no-op implementations, so you only need to
implement the ones relevant to your ad setup.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertDelegate``

## Topics

### Following Page Changes

[`didChangeTo(spread:inEdition:inPublished:)`](/documentation/PSReader/AdvertViewController/didChangeTo(spread:inEdition:inPublished:))

Called by the reader for **editions on PageSuite’s current system**
when the visible page changes.

### Replica Editions

[`didChangeTo(spread:inReplicaEdition:)`](/documentation/PSReader/AdvertViewController/didChangeTo(spread:inReplicaEdition:))

Called by the modern reader for **legacy replica editions** when the
visible page changes.

[`didChangeToIndex(_:)`](/documentation/PSReader/AdvertViewController/didChangeToIndex(_:))

Default no-op implementation. Called by the **legacy replica** reader
via the `PSBannerContent` protocol.

